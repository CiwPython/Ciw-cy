.. _simulation-methods:

================
Dulliau Efelychu
================

Mae yna nifer of ffyrdd i derfynu efelychiad:

- :ref:`until_maxtime`
- :ref:`until_maxcustomers`
- :ref:`until_deadlock`

.. _until_maxtime:

-------------------------------
:code:`simulate_until_max_time`
-------------------------------

Mae'r method yma yn efelychu'r system o system gwag. Mae'r efelychiad yn terfynu unwaith bod swm penodol o amser efelychiad wedi pasio. Mae'r method yn cymryd :code:`max_simulation_time`::

    params = {
        'Arrival_distributions': [['Exponential', 1.0]],
        'Service_distributions': [['Exponential', 0.5]],
        'Number_of_servers': [1],
        'Transition_matrices': [[0.0]],
        'Queue_capacities': [3]
    }
    N = ciw.create_network(params)
    Q = ciw.Simulation(N)

    Q.simulate_until_max_time(100)

Dadleuon allweddair:
 - :code:`max_simulation_time`: ANGENRHEIDIOL. Y swm penodol o amser efelychiad i rhedeg yr efelychiad am.
 - :code:`progress_bar`: OPSIYNNOL. Gweler :ref:`progress-bars`.



.. _until_maxcustomers:

------------------------------------
:code:`simulate_until_max_customers`
------------------------------------

Mae'r method yma yn efelychu'r system o system gwag. Mae'r system yn terfynu unwaith bod nifer penodol o cwsmeriaid wedi pasio trwyddo. Mae'r method yn cymryd :code:`max_customers`::

    params = {
        'Arrival_distributions': [['Exponential', 1.0]],
        'Service_distributions': [['Exponential', 0.5]],
        'Number_of_servers': [1],
        'Transition_matrices': [[0.0]],
        'Queue_capacities': [3]
    }
    N = ciw.create_network(params)
    Q = ciw.Simulation(N)

    Q.simulate_until_max_customers(20, method='Finish')

MAe yn tri dull o efelychi nes bod nifer penodol o cwsmeriaid wedi bod, wedi'i dynodi gan y dadl allweddair :code:`method`.
 - Finish: Efelychu nes bod :code:`max_customers` wedi cyrraedd yr Exit Node.
 - Arrive: Efelychu nes bod :code:`max_customers` wedi'i creu wrth yr Arrival Node.
 - Accept: Efelychu nes bod :code:`max_customers` wedi'i creu ac wedi'i derbyn (heb cael eu wrthod) wrth yr Arrival Node.

Dadleuon allweddair:
 - :code:`max_customers`: ANGENRHEIDIOL. Y nifer macsimwm o cwsmeriaid.
 - :code:`method`: OPSIYNNOL. Dull o cyfri'r cwsmeriaid. Y dull diofyn yw 'Finish'.
 - :code:`progress_bar`: OPSIYNNOL. Gweler :ref:`progress-bars`.


.. _until_deadlock:

-------------------------------
:code:`simulate_until_deadlock`
-------------------------------

Efelychu nes bod y system wedi cyrraedd llwyrglo. Gweler :ref:`deadlock-detection`.