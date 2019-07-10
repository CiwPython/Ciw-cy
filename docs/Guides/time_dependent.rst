.. _timedependent-dists:

============================================================
Sut i Ddiffinio Dosraniadau Amser Dibynnol a Cyflwr Dibynnol
============================================================

Trwy diffinio gwrthrychau dosraniad gwstwm, gallwn diffinio doraniadau amser-dibynnol a cyflwr-dibynnol.
Mae'n hawdd wedyn creu dosraniadau amser-a-cyflwr-dibynnol hefy.

Rhaid i'r gwrthrych dosraniad gwstwm hyn etifeddu o'r dosbarth cyffredinol :code:`ciw.dists.Distribution`, ac mae angen diffinio dull :code:`.sample` sy'n allbynnu yr amser a samplwyd.
Rhaid i'r dull cymryd fel mewnbwn y newidyn amser :code:`t`, ac hefyd yr unigolyn :code:`ind`.


Dosraniadau Amser Dibynnol
--------------------------

Yn Ciw gallwn ddiffinio dosraniadau amser dibynnol, hynny yw dosraniadau amser gwasanaeth neu rhwng-dyfodiad sy'n newid wrth i amser yr efelychiad symud ymlaen.
I wneud hwn mae angen diffinio gwrthrych amser dibynnol, sydd a dull :code:`sample`, sy'n rhoi'r amser a samplwyd.

Er enghraifft, os ydyn ni eisiau dyfodiadau pob 30 munud yn y bore, pob 15 munud amser cinio, pob 45 munud yn y prynhawn, a pob 90 munud trwy'r nos::

    >>> import ciw
    >>> class TimeDependentDist(ciw.dists.Distribution):
    ...     def sample(self, t, ind=None):
    ...         if t % 24 < 12.0:
    ...             return 0.5
    ...         if t % 24 < 14.0:
    ...             return 0.25
    ...         if t % 24 < 20.0:
    ...             return 0.75
    ...         return 1.5

Mae'r dull yma yn rhoi amseroedd rhwng dyfodi o 0.5 awr rhwng canol nos (0) a 13, 0.25 awr rhwng 12 a 14, 0.75 awr rhwng 14 a 20, a 1.5 awr rhwng 20 a chanol nos (24).
Yna mae'n ailadrodd.
I brofi'r ffwythiant::

    >>> D = TimeDependentDist()
    >>> D.sample(9.5)
    0.5
    >>> D.sample(11.0)
    0.5
    >>> D.sample(13.25)
    0.25
    >>> D.sample(17.0)
    0.75
    >>> D.sample(22.0)
    1.5
    >>> D.sample(33.2) # hanner awr wedi 9 y diwrnod nesaf
    0.5

Gadewch i ni weithredu hwn mewn ciw un nod gyda nifer anfeidraidd o weinyddion::

    >>> import ciw
    >>> N = ciw.create_network(
    ...     arrival_distributions=[TimeDependentDist()],
    ...     service_distributions=[ciw.dists.Deterministic(0.0)],
    ...     number_of_servers=['Inf']
    ... )

Yna efelychwn am un diwrnod.
Rydym yn disgwyl 24 dyfodiad yn y bore (12 awr, un pob hanner awr); 8 dyfodiad amser cinio (2 awr, un pob 15 munud); 8 dyfodiad yn y prynhawn (6 awr, un pob 45 munud); a 2 dyfodiad yn y nos (4 awr, un pob awr a hanner).
Felly, disgwylir cyfanswm o 42 cwsmer pasio trwy'r system::

   >>> Q = ciw.Simulation(N)
   >>> Q.simulate_until_max_time(24.0)

   >>> len(Q.nodes[-1].all_individuals)
   42



Dosraniadau Cyflwr Dibynnol
---------------------------

Yn ogystal a'r paramedr amser :code:`t`, mae'r dull samplu yn cymryd mewn yr unigolyn :code:`ind`.
Felly gallwn defnyddio priodweddau'r unigolyn hyn er mwyn samplu amser gwasanaeth (*noder nad yw'n gwneud synnwyr i defnyddio hwn i samplu amseroedd rhwng-dyfodiad oherwydd nad oes unigolyn wedi'i creu eto!*).
Mae gan yr unigolyn hyn priodwedd :code:ind.simulation`, sy'n pwyntio at y gwrthrych :code:`Simulation`, sy'n golygu fod ganddo mynediad i cyflwr y system cyfan.

Nawr gallwn cymryd mantais o hwn i diffinio dosraniadau cyflwr dibynnol.

Fel enghraifft, diffiniwn dosraniad ar gyfer system un nod sy'n rhoi:
    + :code:`0.20` os oes 0 person wrth y nod,
    + :code:`0.15` os oes is 1 person wrth y nod,
    + :code:`0.10` os oes 2 person wrth y nod,
    + :code:`0.05` os oes 3 person wrth y nod,
    + :code:`0.00` otherwise.

Mae hwn yn cyfateb i'r ffwythiant:
    
    $$\max(-0.05n + 0.2, 0)$$

lle :math:`n` yw nifer y cwsmeriaid yn y nod.
Ysgrifennwn dosbarth dosraniad i'w ddefnyddio::

    >>> class StateDependentDist(ciw.dists.Distribution):
    ...     def sample(self, t=None, ind=None):
    ...         n = ind.simulation.nodes[ind.node].number_of_individuals
    ...         return max((-0.05*n) + 0.2, 0)

Nawr i wirio os yw hyn yn gweithio, bydd yr amser gwasanaeth cymedrig tua'n hafal i'r gwerth a chafwyd os cymhwyswn y ffwythiant hyn i'r maint ciw cymedrig::

    >>> N = ciw.create_network(
    ...     arrival_distributions=[ciw.dists.Exponential(4)],
    ...     service_distributions=[StateDependentDist()],
    ...     number_of_servers=[1]
    ... )

    >>> ciw.seed(0)
    >>> Q = ciw.Simulation(N)
    >>> Q.simulate_until_max_time(500)
    >>> recs = Q.get_all_records()

    >>> services = [r.service_time for r in recs if r.arrival_date > 100]
    >>> sum(services) / len(services)
    0.1549304...

    >>> queue_sizes = [r.queue_size_at_arrival for r in recs if r.arrival_date > 100] + [r.queue_size_at_departure for r in recs if r.arrival_date > 100]
    >>> average_queue_size = sum(queue_sizes) / len(queue_sizes)
    >>> (-0.05 * average_queue_size) + 0.2
    0.1547408...
