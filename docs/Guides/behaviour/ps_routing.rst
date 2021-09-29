.. _ps-routing:

======================================================
Ymuno a'r Ciw Byrraf mewn Systemau Rhannu Prosesyddion
======================================================

Yn yr enghraifft hon byddwn yn ystyried nifer o giwiau rhannu prosesyddion paralel, lle mae cwsmeriaid yn cael eu hanfon i'r nod lleiaf brysur. Rydym yn galw hwn System Ymuno a'r Ciw Byrraf, neu system JSQ (*Join Shortest Queue*).

Ystyriwch tri nod rhannu prosesyddion annibynnol, paralel. Mae cwsmeriaid sy'n cyrraed yn cael eu hanfon i'r nod lleiaf brysur.
Gallwn modelu hwn fel system o 4 nod: mae'r nod cyntaf yn ffug-nod lle mae cwsmeriaid yn dyfodi, ac mae'n eu trosglwyddo i un o'r tri nod rhannu prosesyddion sydd weddill.
Os yw'r dosraniad dyfodi yn Poisson gyda chyfradd 8, ac mae'r amseroess gwasanaeth wedi dosranu'n esbonyddol gyda pharamedr 10, yna ein rhwydwaith yw::


    >>> import ciw
    >>> N = ciw.create_network(
    ...     arrival_distributions=[ciw.dists.Exponential(8),
    ...                            ciw.dists.NoArrivals(),
    ...                            ciw.dists.NoArrivals(),
    ...                            ciw.dists.NoArrivals()],
    ...     service_distributions=[ciw.dists.Deterministic(0),
    ...                            ciw.dists.Exponential(10),
    ...                            ciw.dists.Exponential(10),
    ...                            ciw.dists.Exponential(10)],
    ...     number_of_servers=[float('inf'),
    ...                        float('inf'),
    ...                        float('inf'),
    ...                        float('inf')],
    ...     routing=[[0, 0, 0, 0],
    ...              [0, 0, 0, 0],
    ...              [0, 0, 0, 0],
    ...              [0, 0, 0, 0]]
    ... )

Ar gyfer pob un o'r tri nod rhannu prosesyddion paralel, gallwn defnyddio dosbarth :code:`ciw.PSNode`.
Ond, mae nawr angen dosbarth nod gwahanol ar gyfer ein ffug-nod, er mwyn codio'r penderfyniadau trosglwydo. Galwn ni'n dosbarth hwn yn :code:`RoutingDecision`::

    >>> class RoutingDecision(ciw.Node):
    ...     def next_node(self, ind):
    ...         """
    ...         Canfod y nod nesaf trwy edrych ar nodau 2, 3, a 4, i weld
    ...         pa mor brysur ydynt, a trosglwyddo i'r un lleiaf brysur.
    ...         """
    ...         busyness = {n: self.simulation.nodes[n].number_of_individuals for n in [2, 3, 4]}
    ...         chosen_n = sorted(busyness.keys(), key=lambda x: busyness[x])[0]
    ...         return self.simulation.nodes[chosen_n]

Nawr adeiladwn y gwrthrych efelychiad, lle mae'r nod cyntaf yn defnyddio ein dosbarth :code:`RoutingDecision`, ac mae'r gweddill yn defnyddio :code:`ciw.PSNode`. Hefyd ychwanegwn traciwr cyflwr ar gyfer y dadansoddiad::

    >>> ciw.seed(0)
    >>> Q = ciw.Simulation(
    ...     N, tracker=ciw.trackers.SystemPopulation(),
    ...     node_class=[RoutingDecision, ciw.PSNode, ciw.PSNode, ciw.PSNode])

Rehdwn ni hwn ar gyfer 100 uned amser::

    >>> Q.simulate_until_max_time(100)

Gallwn edrych ar y tebygolrwyddau cyflwr, hynny yw, cyfran yr amser mae'r system wedi gwario ym mhob cyflwr, lle mae cyflwr yn dynodi nifer o gwsmeriaid sydd yn bresenol yn y system::

    >>> Q.statetracker.state_probabilities(observation_period=(10, 90)) # doctest:+SKIP
    {0: 0.425095024227593,
     1: 0.35989517302304014,
     2: 0.14629711075255158,
     3: 0.054182634504608064,
     4: 0.01124224242623659,
     5: 0.002061285633093934,
     6: 0.0012265294328765105}
