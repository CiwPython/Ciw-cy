.. _set-seed:

================
Sut i Osod Hedyn
================

I sicrhau ailgynhyrchioldeb canlyniadau gall defnyddwyr gosod hedyn ar gyfer holl lifoedd haprif mae Ciw yn defnyddio.
Gallwch wneud hwn gan ddefnyddio’r ffwythiant :code:`ciw.seed`::
    
    >>> import ciw
    >>> ciw.seed(5)

Nodwch oherwydd samplo wrth ymgychwyn, mae angen gosod yr hedyn **cyn** creu'r gwrthrych :code:`ciw.Simulation`.

Fel enghraifft, cymerwch y rhwydwaith canlynol::

    >>> N = ciw.create_network(
    ...     arrival_distributions=[ciw.dists.Exponential(5)],
    ...     service_distributions=[ciw.dists.Exponential(10)],
    ...     number_of_servers=[1]
    ... )

Rhedwch y system am 20 uned amser, yn defnyddio hedyn o 1, a ffeindiwch yr amser aros cymedrig::

    >>> ciw.seed(1)
    >>> Q = ciw.Simulation(N)
    >>> Q.simulate_until_max_time(20)
    >>> waits = [r.waiting_time for r in Q.get_all_records()]
    >>> sum(waits)/len(waits)
    0.0824058654563...

Yn defnyddio'r un hedyn eto, mae'r union un amser aros cymedrig yn achosi’r union un canlyniad::

    >>> ciw.seed(1)
    >>> Q = ciw.Simulation(N)
    >>> Q.simulate_until_max_time(20)
    >>> waits = [r.waiting_time for r in Q.get_all_records()]
    >>> sum(waits)/len(waits)
    0.0824058654563...

Nawr, yn defnyddio hedyn gwahanol, fe geir canlyniad gwahanol::

    >>> ciw.seed(2)
    >>> Q = ciw.Simulation(N)
    >>> Q.simulate_until_max_time(20)
    >>> waits = [r.waiting_time for r in Q.get_all_records()]
    >>> sum(waits)/len(waits)
    0.1691349404558...
