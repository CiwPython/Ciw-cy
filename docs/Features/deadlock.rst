.. _deadlock-detection:

=========================
Y Gallu i Ganfod Llwyrglo
=========================

Mae gan Ciw'r gallu i ganfod llwyrglo. Gyda Ciw gall efelychu rhwydwaith ciwio nes iddo gyrraedd llwyrglo.
Yna mae Ciw yn recordio'r amser nes cyrraedd llwyrglo o bob cyflwr.

Er mwyn cymryd mantais o'r nodwedd yma, gosodwch opsiwn canfod llwyrglo i un o'r canfodyddion llwyrglo wrth greu'r gwrthrych Simulation::

    >>> Q = ciw.Simulation(N, deadlock_detector='StateDigraph') # doctest:+SKIP

Yna defnyddiwch y method :code:`simulate_until_deadlock`. Mae'r priodwedd :code:`times_to_deadlock` yn cynnwys yr amseroedd nes llwyrglo o bob cyflwr (lle recordiwyd y cyflwr gan :ref:`state-tracker`)::

    >>> import ciw
    >>> N = ciw.create_network(params) # doctest:+SKIP
    >>> Q = ciw.Simulation(N, deadlock_detector='StateDigraph') # doctest:+SKIP
    >>> Q.simulate_until_deadlock() # doctest:+SKIP
    >>> times = Q.times_to_deadlock # doctest:+SKIP

lle mae :code:`times` yn eiriadur gyda chyflyrau fel allweddu ac amseroedd fel gwerthoedd.



---------------------
Enghraifft - Llwyrglo
---------------------

Ystyriwch y ciw M/M/1/3 lle mae gan gwsmeriaid tebygolrwydd 0.5 o ailymuno a'r ciw ar ôl gwasanaeth. Os yw'r ciw yn llawn yna mae'r cwsmer yna yn cael ei flocio, felly mae'r system yn cyrraedd llwyrglo.

Paramedrau::

    >>> params = {'Arrival_distributions': {'Class 0': [['Exponential', 6.0]]},
    ...           'Number_of_nodes': 1,
    ...           'Number_of_servers': [1],
    ...           'Queue_capacities': [3],
    ...           'Number_of_classes': 1,
    ...           'Service_distributions': {'Class 0': [['Exponential', 5.0]]},
    ...           'Transition_matrices': {'Class 0': [[0.5]]}}

Rhedeg nes cyrraedd llwyrglo::

    >>> import ciw
    >>> ciw.seed(99)
    >>> N = ciw.create_network(params)
    >>> Q = ciw.Simulation(N, deadlock_detector='StateDigraph')
    >>> Q.simulate_until_deadlock()
    >>> self.times_to_deadlock # doctest:+SKIP
    {((1, 0),): 1.0845416939916719, ((3, 0),): 0.5436399978272065, ((0, 0),): 1.1707879982560288, ((4, 0),): 0.15650986183172932, ((3, 1),): 0.0, ((2, 0),): 1.0517097907100657}

Fan hyn mae'r cyflwr :code:`((i, j),)` yn dynodi'r cyflwr lle mae `i` cwsmer yn y nod a `j` o rain wedi'i flocio.