.. _timedependent-dists:

==========================================
Sut i Ddiffinio Dosraniadau Amser Dibynnol
==========================================

Yn Ciw gallwn ddiffinio dosraniadau amser dibynnol, hynny yw dosraniadau amser gwasanaeth neu rhwng-dyfodiad sy'n newid wrth i amser yr efelychiad symud ymlaen.
I wneud hwn mae angen diffinio ffwythiant amser dibynnol, sy'n rhoi'r amser a samplwyd.
Rhaid i hwn cymryd y newidyn amser `t`.

Er enghraifft, os ydyn ni eisiau dyfodiadau pob 30 munud yn y bore, pob 15 munud amser cinio, pob 45 munud yn y prynhawn, a pob 90 munud trwy'r nos::

    >>> def time_dependent_function(t):
    ...     if t % 24 < 12.0:
    ...         return 0.5
    ...     if t % 24 < 14.0:
    ...         return 0.25
    ...     if t % 24 < 20.0:
    ...         return 0.75
    ...     return 1.5

Mae'r ffwythiant yma yn rhoi amseroedd rhwng dyfodi o 0.5 awr rhwng canol nos (0) a 13, 0.25 awr rhwng 12 a 14, 0.75 awr rhwng 14 a 20, a 1.5 awr rhwng 20 a chanol nos (24).
Yna mae'n ailadrodd.
I brofi'r ffwythiant::

    >>> time_dependent_function(9.5)
    0.5
    >>> time_dependent_function(11.0)
    0.5
    >>> time_dependent_function(13.25)
    0.25
    >>> time_dependent_function(17.0)
    0.75
    >>> time_dependent_function(22.0)
    1.5
    >>> time_dependent_function(33.2) # hanner wedi 9 y diwrnod nesaf
    0.5

Gadewch i ni weithredu hwn mewn ciw un nod gyda nifer anfeidraidd o weinyddion::

    >>> import ciw
    >>> N = ciw.create_network(
    ...     Arrival_distributions=[['TimeDependent', time_dependent_function]],
    ...     Service_distributions=[['Deterministic', 0.0]],
    ...     Number_of_servers=['Inf']
    ... )

Yna efelychwn am un diwrnod.
Rydym yn disgwyl 24 dyfodiad yn y bore (12 awr, un pob hanner awr); 8 dyfodiad amser cinio (2 awr, un pob 15 munud); 8 dyfodiad yn y prynhawn (6 awr, un pob 45 munud); a 2 dyfodiad yn y nos (4 awr, un pob awr a hanner).
Felly, disgwylir cyfanswm o 42 cwsmer pasio trwy'r system::

   >>> Q = ciw.Simulation(N)
   >>> Q.simulate_until_max_time(24.0)

   >>> len(Q.nodes[-1].all_individuals)
   42
