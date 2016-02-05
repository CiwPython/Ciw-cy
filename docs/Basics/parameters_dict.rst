.. _parameters-dict:

======================
Y Geiriadur Paramedrau
======================

Er mwyn ddiffinio efelychiad rhwydwaith ciwio yn llawn, angen diffinio'r canlynol:

- Nifer o nodau (gorsafoedd gwasanaeth)
- Nifer o ddosbarthau cwsmer
- Amser rhedeg yr efelychiad

Ar gyfer pob nod mae angen diffinio; canlynol (yn annibynnol o ddosbarth cwsmer):

- Nifer o weinyddion
- Cynhwysedd ciwio

Yna, ar gyfer pob nod a phob dosbarth cwsmer, rhaid ddiffinio'r canlynol:

- Cyfradd dyfodiad
- Dosraniad amser gwasanaeth

Ac mae pob dosbarth cwsmer angen:

- Matrics trosglwyddiadau

Dangosir esiampl lawn o eiriadur paramedrau ar gyfer rhwydwaith tri nod gyda dau ddosbarth cwsmer isod:

    >>> params = {'Arrival_distributions': {'Class 1': [['Exponential', 1.0], ['Exponential', 1.8], ['Exponential', 7.25]],
    ...                             'Class 0': [['Exponential', 6.0], ['Exponential', 4.5], ['Exponential', 2.0]]},
    ...           'Number_of_nodes': 3,
    ...           'detect_deadlock': False,
    ...           'Simulation_time': 2500,
    ...           'Number_of_servers': [2, 1, 1],
    ...           'Queue_capacities': ['Inf', 'Inf', 10],
    ...           'Number_of_classes': 2,
    ...           'Service_distributions': {'Class 1': [['Exponential', 8.5], ['Triangular', 0.1, 0.8, 0.95], ['Exponential', 3.0]],
    ...                                     'Class 0': [['Exponential', 7.0], ['Exponential', 5.0], ['Gamma', 0.4, 0.6]]},
    ...  'Transition_matrices': {'Class 1': [[0.7, 0.05, 0.05], [0.5, 0.1, 0.4], [0.2, 0.2, 0.2]],
    ...                          'Class 0': [[0.1, 0.6, 0.2], [0.0, 0.5, 0.5], [0.3, 0.1, 0.1]]}}


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

Yn y matrics trosglwyddo yma mae'r elfen `(i,j)`ed yn cyfateb a'r tebygolrwydd o drosglwyddo i nod `j` ar ôl wasanaeth yn nod `i`.

Mae yna nifer o nodweddion eraill, gweler :ref:`features` am ragor o wybodaeth.

Fe all allweddau'r geiriadur hefyd cael ei ddefnyddio fel dadlau allweddair wrth ddiffinio efelychiad. Mae gan Ciw ffwythiant i lwytho'r paramedrau hyn o ffeil, gweler :ref:`parameters-file`.
