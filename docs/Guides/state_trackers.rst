.. state-trackers:

=============================
Sut i Dracio Clyflwr y System
=============================

Cyflwr y system yw gyfluniad yr unigolion o amgylch y system. Gall cael ei mesur mewn nifer o ffyrdd wahanol - er enghraiff, gall cyflwr system bod nifer o gwsmeriaid sy'n aros ym mhob nod.

Mae gan Ciw yr opsiwn i gychwyn draciwr cyflwr (:code:`tracker`) er mwyn tracio cyflwr y system wrth i'r efelychiad mynd yn ei flaen. Mae gan y dracwyr hyn nifer o ddefnyddiau: gallwch cael holl hanes cyflwr y system, o hyn gallwch cael tebygolrwyddau cyflwr, ac mae ganddo defnydd wrth archwilio i mewn i lwyrglo.

Y draciwr diofyn yw'r :code:`StateTrack` nad yw'n gwneud dim.
Mae nifer o dracwyr cyflwr eraill y gallwch eu defnyddio, sy'n recordio cyflwr y system mewn nifer o ffyrdd. Mae'r gwrthrychau hyn yn etifeddu o'r dosbarth sylfaenol :code:`StateTracker`, ac felly gall tracwyr cyflwyr newydd cael eu ysgrifennu yn yr un modd.
Ar gyfer rhestr ac esboniad o'r holl dracwyr cyflwr sydd gan Ciw ar hyn o bryd, gweler :ref:`refs-statetrackers`.

Enghraifft: ystyriwch ciw M/M/1. Mae'r traciwr :code:`SystemPopulation` yn diffinio cyflwr fel y nifer o unigolion sydd yn y system::

    >>> import ciw
    >>> N = ciw.create_network(
    ...    arrival_distributions=[ciw.dists.Exponential(0.1)],
    ...    service_distributions=[ciw.dists.Exponential(0.2)],
    ...    number_of_servers=[1]
    ... )

    >>> ciw.seed(1)
    >>> Q = ciw.Simulation(N,
    ...     tracker=ciw.trackers.SystemPopulation()
    ... )
    >>> Q.simulate_until_max_time(250)

Nawr gallwn weld hanes y system::

    >>> Q.statetracker.history # doctest:+SKIP
    [[0.0, 0],
     [1.44291..., 1],
     [10.84369..., 0],
     [15.87259..., 1],
     [17.34491..., 0],
     [22.71318..., 1],
     [25.69774..., 0],
     ...
    ]                                  

Mae hyn yn dangos roedd y system mewn cyflwr :code:`0` o amser 0.0 i 1.44291, roedd mewn cyflwr :code:`1` o amser 1.44291 i 10.84369, aeth nôl i gyflwr :code:`0` o 10.84369 i amser 15.87259, ac yn y blaen.

O hwn gallwn cael cyfrannau'r amser yr oedd y system ym mhob cyflwr::

    >>> Q.statetracker.state_probabilities() # doctest:+SKIP
    {0: 0.55425..., 1: 0.24676..., 2: 0.13140..., 3: 0.06757...}

Felly roedd y system mewn cyflwr :code:`0` (dim unigolion yn y system) 55.4% o'r amser, mewn cyflwr :code:`1` (un unigolyn yn y system) 24.7% o'r amser, cyflwr :code:`2` (dau unigolyn yn y system) 13.1% o'r amser, a chyflwr :code:`3` (tri unigolyn yn y system) 6.8% o'r amser.

Os oes angen amser-twymo ac amser-oeri wrth gyfrifo'r tebygolrwyddau cyflwr, gallwn mewnbynnu cyfnod arsylwi. Er enghraifft, os hoffwn canfod cyfrannau'r amser yr oedd y system ym mhob cyflwr, rhwng dyddiadau :code;`50` ac :code:`200`, yna gallwn defnyddio'r canlynol::

    >>> Q.statetracker.state_probabilities(observation_period=(50, 200)) # doctest:+SKIP

Nodwch bod tracwyr gwahanol yn cynrychioli gwahanol cyflyriau mewn gwahanol ffyrdd, gweler :ref:`refs-statetrackers` ar gyfer rhestr o'r holl dracwyr.