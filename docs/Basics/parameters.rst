.. _parameters-file:

==================
Y Ffeil Paramedrau
==================

Mae Ciw yn cynnwys ffwythiant :code:`load_parameters` sy'n llwytho ffeil paramedrau fel geiriadur. Mae'r ffeil yma mewn fformat :code:`.yml`.

Dangosir esiampl lawn o ffeil paramedrau ar gyfer rhwydwaith tri nod gyda dau ddosbarth cwsmer isod::

    Arrival_distributions:
      Class 0:
      - - Exponential
        - 6.0
      - - Exponential
        - 4.5
      - - Exponential
        - 2.0
      Class 1:
      - - Exponential
        - 1.0
      - - Exponential
        - 1.8
      - - Exponential
        - 7.25
    detect_deadlock: False
    Number_of_classes: 2
    Number_of_nodes: 3
    Number_of_servers:
    - 2
    - 1
    - 1
    Queue_capacities:
    - "Inf"
    - "Inf"
    - 10
    Service_distributions:
      Class 0:
      - - Exponential
        - 7.0
      - - Exponential
        - 5.0
      - - Gamma
        - 0.4
        - 0.6
      Class 1:
      - - Exponential
        - 8.5
      - - Triangular
        - 0.1
        - 0.8
        - 0.95
      - - Exponential
        - 3.0
    Simulation_time: 2500
    Transition_matrices:
      Class 0:
      - - 0.1
        - 0.6
        - 0.2
      - - 0.0
        - 0.5
        - 0.5
      - - 0.3
        - 0.1
        - 0.1
      Class 1:
      - - 0.7
        - 0.05
        - 0.05
      - - 0.5
        - 0.1
        - 0.4
      - - 0.2
        - 0.2
        - 0.2

Mae enwau'r newidynnau union yr un fath ag allweddau'r geiriadur paramedrau (:ref:`parameters-dict`), a'r dadlau allweddair a all cael ei ddefnyddio.