.. _tutorial-v:

================================
Tiwtorial V: Rhwydwaith o Ciwiau
================================

Mae pŵer go iawn Ciw yn dod wrth modelu rhwydwaith o ciwiau.
Hynny yw nifer o nodau gwasanaeth, fel bod pan mae cwsmer yn gorffen gwasanaeth, mae yna tebygolrwydd o ymuno a nod arall, ail-ymuno a'r nod presennol, neu gadael y system.

Dychmygwch caffi sy'n gwerthu bwyd poeth ac oer.
Gall cwsmeriaid cymryd nifer o llwybrau:

+ Mae angen i cwsmeriaid sydd ond eisiau bwyd oer ciwio wrth y cownter bwyd oer, ac yna cymryd eu bwyd i'r til i talu.
+ Mae angen i cwsmeriaid sydd ond eisiau bwyd poeth ciwio with y cownter bwyd poeth, ac yna cymryd eu bwyd i'r til i talu.
+ Mae angen i cwsmeriaid sydd eisiau bwyd oer a bwyd poeth ciwio yn gyntaf ar gyfer bwyd oer, yna ar gyfer bwyd poeth, ac yna cymryd y ddau i'r til i talu.

Yn y system yma mae yna tri nod: Cownter bwyd oer (Nod 1), Cownter bwyd poeth (Nod 2), a'r til (Nod 3):

+ Mae cwsmeriaid sydd ond eisiau bwyd poeth yn cyrraedd ar gyfradd 12 yr awr.
+ Mae cwsmeriaid sydd eisiau bwyd oer yn cyrraedd ar gyfradd 18 yr awr.
+ Mae 30% o'r holl cwsmeriaid sydd eisiau prynu bwyd oer hefyd eisiau prynu bwyd poeth.
+ Ar gyfartaledd mae'n cymryd 1 munud i weinu bwyd oer, 2 a hanner munud i weinu bwyd poeth, a 2 munud i talu.
+ Mae yna 1 gweinydd wrth y cownter bwyd oer, 2 weinydd wrth y cownter bwyn poeth, a 2 weinydd wrth y til.

Dangosir diagram o'r system isod:

.. image:: ../_static/cafe.svg
   :scale: 100 %
   :alt: Diagram o'r rhwydwaith ciwio caffi.
   :align: center

Gellir disgrifio'r system yma mewn un gwrthrych Network.
Rhestrir y dosraniadau dyfodi a gwasanaeth a nifer y weinyddion yn trefn y nodau.
Mae hefyd angen *matrics trosglwyddo*.

Matrics trosglwyddo yw matrics :math:`n \times n` (lle :math:`n` yw nifer y nodau yn y rhwydwaith) fel bod yr elfen :math:`(i,j)\text{fed}` yn cyfateb i'r tebygolrwydd o trosglwyddo i nod :math:`j` ar ol gorffen wasanaeth yn nod :math:`i`.
Mae matrics trosglwyddo'r caffi yn edrych fel hyn:

.. math::

    \begin{pmatrix}
    0.0 & 0.3 & 0.7 \\
    0.0 & 0.0 & 1.0 \\
    0.0 & 0.0 & 0.0 \\
    \end{pmatrix}


Hynny yw mae 30% o'r cwsmeriaid bwyd oer yn mynd ymlaen i'r cownter bwyd poeth, tra bod y 70% sy'n weddill yn mynd i'r till, ac mae 100% o cwsmeriaid bwyd poeth yn mynd ymlaen i'r til.
Felly mae Network y caffi yn edrych fel hyn::

    >>> import ciw
    >>> N = ciw.create_network(
    ...     Arrival_distributions=[['Exponential', 0.3],
    ...                            ['Exponential', 0.2],
    ...                            'NoArrivals'],
    ...     Service_distributions=[['Exponential', 1.0],
    ...                            ['Exponential', 0.4],
    ...                            ['Exponential', 0.5]],
    ...     Transition_matrices=[[0.0, 0.3, 0.7],
    ...                          [0.0, 0.0, 1.0],
    ...                          [0.0, 0.0, 0.0]],
    ...     Number_of_servers=[1, 2, 2]
    ... )

Sylwch y dosraniadau dyfodi:
mae 18 dyfodiad bwyd oer yn cyfatebol i :code:`0.3` y munud; mae 12 dyfodiad bwyd poeth yn cyfatebol i :code:`0.2` y munud; a nid oes unrhyw dyfodiadau wrth y til.

Sylwch y dosraniadau gwasanaeth:
mae amser gwasanaeth bwyd oer cymedrig o 1 munud yn cyfatebol i cyfradd o 1/1 = :code:`1` gwasanaeth y munud; mae amser gwasanaeth bwyd poeth cymedrig o 2.5 munud yn cyfatebol i 1/2.5 = :code:`0.4` gwasanaeth y munud; ac mae amser gwasanaeth cymedrig o 2 munud with y til yn cyfatebol i :code:`0.5` gwasanaeth y munud.

Gadewch i ni efelychu'r system yma am un sifft amser cinio o 3 awr (180 munud).
Ar dechrau amser cinio mae'r caffi yn agor, felly mae'r system yn dechrau yn gwag.
Felly nad oes angen amser-cynhesu.
Defnyddiwn 20 munud o amser-oeri.
Rhedwn 10 arbrawf, i cael mesur nifer cymedrig cwsmeriaid sy'n pasio trwy'r system.
I ffeindio'r nifer cymedrig o cwsmeriaid sy'n pasio trwy'r system, gallwn cyfri'r nifer o gofnodion data sydd wedi pasio trwy Nod 3 (y til)::

    >>> completed_custs = []
    >>> for trial in range(10):
    ...     ciw.seed(trial)
    ...     Q = ciw.Simulation(N)
    ...     Q.simulate_until_max_time(200)
    ...     recs = Q.get_all_records()
    ...     num_completed = len([r for r in recs if r.node==3 and r.arrival_date < 180])
    ...     completed_custs.append(num_completed)

Nawr gallwn cael nifer cymedrig o cwsmeriaid sydd wedi pasio trwy'r system::

    >>> sum(completed_custs) / len(completed_custs)
    83.0

Felly rydym wedi defnyddio Ciw i ffeindio fod y caffi medru weinu nifer cyfataledd o 83 cwsmer mewn sifft amser cinio o tri awr.