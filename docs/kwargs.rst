.. _parameters-list:

=======================
Rhestr Llawn Paramedrau
=======================

Fan hyn mae rhestr lawn y paramedrau a all geiriadur paramedrau ei gymryd, gyda disgrifiad o'r gwerthoedd hanfodol. Os ydych yn defnyddio ffeil paramedrau, dyma'r opsiynau a'r gwerthoedd sydd angen yn y ffeil :code:`.yml`.


Arrival_distributions
~~~~~~~~~~~~~~~~~~~~~

*Angenrheidiol*

Disgrifir y dosraniadau rhwng-dyfodiad ar gyfer pob nod a pob dosbarth cwsmer.
Geiriadur yw hwn, gyda allweddi fel dosbarthiadau cwsmer, a'i werthoedd yw rhestrau yn disgrifio'r dosraniadau rhwng-dyfodiad ar gyfer pob nod. Os defnyddir un dosbarth cwsmer yn unig gallwch rhoi rhestr o dosraniadau rhwng-dyfodiad. Am fwy o manylion ar dosraniadau, gweler :ref:`service-distributions`.

Dangosir engrhaifft::

    'Arrival_distributions': {'Class 0': [['Exponential', 2.4],
                                          ['Uniform', 0.3, 0.5]],
                              'Class 1': [['Exponential', 3.0],
                                          ['Deterministic', 0.8]]}

Enghraiff o lle ond un dosbarth cwsmer sydd angen::

    'Arrival_distributions': [['Exponential', 2.4],
                              ['Exponential', 2.0]]


Class_change_matrices
~~~~~~~~~~~~~~~~~~~~~

*Opsiynnol*

Geiriadur o matricsau newid dosbarth ar gyfer pob nod. Am fwy o manylion gweler :ref:`dynamic-classes`.

Engrhaifft ar gyfer rhwydwaith dau nod gyda dau dosbarth cwsmer::

    'Class_change_matrices': {'Node 0': [[0.3, 0.4, 0.3],
                                         [0.1, 0.9, 0.0],
                                         [0.5, 0.1, 0.4]],
                              'Node 1': [[1.0, 0.0, 0.0],
                                         [0.4, 0.5, 0.1],
                                         [0.2, 0.2, 0.6]]}


Number_of_classes
~~~~~~~~~~~~~~~~~

*Opsiynnol*

Dynodir nifer o dosbarthau cwsmer yn yr efelychiad. Os nad ydy wedi'i cynnwys, mae Ciw yn cyfrifo hwn o'r opsiwn :code:`Arrival_distributions`.

Engrhaifft::
    'Number_of_classes': 3


Number_of_nodes
~~~~~~~~~~~~~~~

*Opsiynnol*

Dynodir nifer o nodau yn y rhwydwaith ciwio. Os nad ydy wedi'i cynnwys, mae Ciw yn cyfrifo hwn o'r opsiwn :code:`Number_of_servers`.

Engrhaifft::
    'Number_of_nodes': 6


Number_of_servers
~~~~~~~~~~~~~~~~~

*Angenrheidiol*

Rhestr o'r nifer o weinyddion wrth ymyl pob nod. Os defnyddir amserlen gwaith, rhowch enw'r amserlen yn lle rhif. Am fwy o manylion ar amserlenni gwaith, gweler :ref:`server-schedules`. Rhoddir gwerth 'Inf' os oes angen nifer anfeidraidd o weinyddion.

Engrhaifft::

    'Number_of_servers': [1, 2, 'Inf', 1, 'my_server_schedule']


Queue_capacities
~~~~~~~~~~~~~~~~

*Opsiynnol*

Rhestr o'r cynhwyseddau ciwio macsimum ar gyfer pob nod. Os nad ydy wedi'i cynnwys, y werthoedd diofyn yw 'Inf' ar gyfer pob bod.

Engrhaifft::

    'Queue_capacities': [5, 'Inf', 'Inf', 10]


Service_distributions
~~~~~~~~~~~~~~~~~~~~~

*Angenrheidiol*

Disgrifir y dosraniadau gwasanaeth ar gyfer pob nod a pob dosbarth cwsmer.
Geiriadur yw hwn, gyda allweddi fel dosbarthiadau cwsmer, a'i werthoedd yw rhestrau yn disgrifio'r dosraniadau gwasanaeth ar gyfer pob nod. Os defnyddir un dosbarth cwsmer yn unig gallwch rhoi rhestr o dosraniadau gwasanaeth. Am fwy o manylion ar dosraniadau, gweler :ref:`service-distributions`.

Dangosir engrhaifft::

    'Service_distributions': {'Class 0': [['Exponential', 4.4],
                                        ['Uniform', 0.1, 0.9]],
                            'Class 1': [['Exponential', 6.0],
                                        ['Lognormal', 0.5, 0.6]]}

Enghraiff o lle ond un dosbarth cwsmer sydd angen::

    'Service_distributions': [['Exponential', 4.8],
                            ['Exponential', 5.2]]



Transition_matrices
~~~~~~~~~~~~~~~~~~~

*Angenrheidiol*

Disgrifir y matrics trosglwyddo ar gyfer pob dosbarth cwsmer.
Geiriadur yw hwn, gyda allweddi fel dosbarthau cwsmer, a'r gwerthoedd yw rhestrau o rhestrau (matricsau) yn cynnwys y tebygolrwyddau trosglwyddo. Os defnyddir un dosbarth cwsmer yn unig, gall mewnbynnu matrics trosglwyddo yn unig (rhestr o rhestrau).

Dangosir engrhaifft::

    'Transition_matrices': {'Class 0': [[0.1, 0.3],
                                        [0.0, 0.8]],
                            'Class 1': [[0.0, 1.0],
                                        [0.0, 0.0]]}

Enghraiff o lle ond un dosbarth cwsmer sydd angen::

    'Transition_matrices': [[0.5, 0.3],
                            [0.2, 0.6]]

Engrhaifft o rhwydwaith un node gyda un dosbarth cwsmer::

    'Transition_matrices': [[0.0]]