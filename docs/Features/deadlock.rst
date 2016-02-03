.. _deadlock-detection:

=========================
Y Gallu i Ganfod Llwyrglo
=========================

Mae gan Ciw'r gallu i ganfod llwyrglo. Gyda Ciw gall efelychu rhwydwaith ciwio nes iddo gyrraedd llwyrglo.
Yna mae Ciw yn recordio'r amser nes cyrraedd llwyrglo o bob cyflwr.

Er mwyn cymryd mantais o'r nodwedd yma, gosodwch opsiwn canfod llwyrglo i True yn y ffeil paramedrau::

    detect_deadlock: True

Yna defnyddiwch y method :code:`simulate_until_deadlock` i ddychwelyd yr amseroedd nes llwyrglo o bob cyflwr::

   >>> import ciw
   >>> Q = ciw.Simulation(deadlock_params) # doctest:+SKIP
   >>> times = Q.simulate_until_deadlock() # doctest:+SKIP

lle mae :code:`times` yn eiriadur gyda chyflyrau fel allweddu ac amseroedd fel gwerthoedd. Noder anwybyddwyd :code:`Simulation_time` yn yr achos yma.



---------------------
Enghraifft - Llwyrglo
---------------------

Ystyriwch y ciw M/M/1/3 lle mae gan gwsmeriaid tebygolrwydd 0.5 o ailymuno a'r ciw ar ôl gwasanaeth. Os yw'r ciw yn llawn yna mae'r cwsmer yna yn cael ei flocio, felly mae'r system yn cyrraedd llwyrglo.

Paramedrau::

    >>> params = {'Arrival_rates': {'Class 0': [6.0]},
    ...           'Number_of_nodes': 1,
    ...           'detect_deadlock': True,
    ...           'Simulation_time': 2500,
    ...           'Number_of_servers': [1],
    ...           'Queue_capacities': [3],
    ...           'Number_of_classes': 1,
    ...           'Service_distributions': {'Class 0': [['Exponential', 5.0]]},
    ...           'Transition_matrices': {'Class 0': [[0.5]]}}

Rhedeg nes cyrraedd llwyrglo::

    >>> import ciw
    >>> from random import seed
    >>> seed(99)
    >>> Q = ciw.Simulation(params)
    >>> times = Q.simulate_until_deadlock()
    >>> times # doctest:+SKIP
    {((1, 0),): 1.0845416939916719, ((3, 0),): 0.5436399978272065, ((0, 0),): 1.1707879982560288, ((4, 0),): 0.15650986183172932, ((3, 1),): 0.0, ((2, 0),): 1.0517097907100657}

Fan hyn mae'r cyflwr :code:`((i, j),)` yn dynodi'r cyflwr lle mae `i` cwsmer yn y nod a `j` o rain wedi'i flocio.