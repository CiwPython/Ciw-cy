.. _sim-parameters:

=======================
Paramedrau'r Efelychiad
=======================

Er mwyn ddiffinio efelychiad rhwydwaith ciwio yn llawn, angen diffinio'r canlynol:

- Nifer o nodau (gorsafoedd gwasanaeth)
- Nifer o ddosbarthau cwsmer

Ar gyfer pob nod mae angen diffinio; canlynol (yn annibynnol o ddosbarth cwsmer):

- Nifer o weinyddion
- Cynhwysedd ciwio

Yna, ar gyfer pob nod a phob dosbarth cwsmer, rhaid ddiffinio'r canlynol:

- Cyfradd dyfodiad
- Dosraniad amser gwasanaeth

Ac mae pob dosbarth cwsmer angen:

- Matrics trosglwyddiadau


Dangosir rhestr llawn o'r baramedrau all wrthrych Simulation yn Ciw cymryd yma: :ref:`parameters-list`.
Noder:

- Gall osod :code:`Queue_capacities` i fod yn :code:`"Inf"`.
- Pan nad ydy :code:`Queue_capacities` wedi'i osod i :code:`"Inf"` mae rheolau blocio yn gymwys. Mae blocio Fath I (blocio ar ôl wasanaeth) yn gymwys fan hyn.
- Gall osod :code:`Number_of_servers` i fod yn :code:`"Inf"` hefyd.
- I fedru cael dim dyfodiadau, gosodwch :code:`Arrival_distributions` i :code:`'NoArrivals'`.
- Mae yna nifer of dosraniadau amser gwasanaeth ar gael, gweler :ref:`service-distributions`.
- Mae adran :code:`Transition_matrices` ar gyfer :code:`Class 0` yn cynrychioli’r matrics trosglwyddo canlynol::

   [[0.1, 0.6, 0.2],
    [0.0, 0.5, 0.5],
    [0.3, 0.1, 0.1]]

Yn y matrics trosglwyddo yma mae'r elfen `(i,j)` ed yn cyfateb a'r tebygolrwydd o drosglwyddo i nod `j` ar ôl wasanaeth yn nod `i`.

Mae yna nifer o nodweddion eraill, gweler :ref:`features` am ragor o wybodaeth.

Mae yna dau ffordd o fewnbynnu paramedrau i wrthrych Simulation:

* :ref:`params_dict`
* :ref:`params_file`


.. _params_dict:

--------------------
Geiriadur Paramedrau
--------------------

Fe all wrthrych Simulation cymryd geiriadur yn cynnwys holl kwargs fel allweddi. Dangosir engrhaifft::

    >>> import ciw
    >>> params = {
    ... 'Arrival_distributions': {'Class 0': [['Exponential', 6.0], ['Exponential', 2.5]]},
    ... 'Number_of_nodes': 2,
    ... 'Number_of_servers': [1, 1],
    ... 'Queue_capacities': ['Inf', 4],
    ... 'Number_of_classes': 1,
    ... 'Service_distributions': {'Class 0': [['Exponential', 8.5], ['Exponential', 5.5]]},
    ... 'Transition_matrices': {'Class 0': [[0.0, 0.2], [0.1, 0.0]]}
    ... }
    >>> N = ciw.create_network(params)
    >>> Q = ciw.Simulation(N)


.. _params_file:

----------------
Ffeil Paramedrau
----------------

Mae Ciw yn cynnwys ffwythiant :code:`load_parameters` sy'n llwytho ffeil paramedrau fel geiriadur. Mae'r ffeil yma mewn fformat :code:`.yml`. Dangosir engrhaifft::

    parameters.yml
    
    Arrival_distributions:
      Class 0:
      - - Exponential
        - 6.0
      - - Exponential
        - 2.5
    Number_of_classes: 1
    Number_of_nodes: 2
    Number_of_servers:
    - 1
    - 1
    Queue_capacities:
    - "Inf"
    - 4
    Service_distributions:
      Class 0:
      - - Exponential
        - 8.5
      - - Exponential
        - 5.5
    Transition_matrices:
      Class 0:
      - - 0.0
        - 0.2
      - - 0.1
        - 0.0

Ac yna i'w llwytho i mewn::

    >>> import ciw
    >>> N = ciw.create_network('parameters.yml') # doctest:+SKIP
    >>> Q = ciw.Simulation(N) # doctest:+SKIP

Mae enwau'r newidynnau union yr un fath ag allweddau'r geiriadur paramedrau.