.. _refs-params:

=================
Rhestr Paramedrau
=================

Isod rhestrwyd holl baramedrau mae'r ffwythiant :code:`create_network` yn cymryd, ynghyd â disgrifiadau o'r gwerthoedd a chymerwyd.
Os ddefnyddir ffeil paramedrau, yna dyma ddadleuon a gwerthoedd sydd angen yn y ffeil :code:`.yml`.


Arrival_distributions
~~~~~~~~~~~~~~~~~~~~~

*Angenrheidiol*

Mae'n disgrifio'r dosraniadau rhwng-dyfodiad ar gyfer pob nod a pob dosbarth cwsmer.
Geiriadur yw hwn gyda dosbarthiadau cwsmer fel allweddau, a rhestrau yn disgrifio dosraniadau rhwng-dyfodiad pob nod fel gwerthoedd.
Os ond un dosbarth cwsmer sydd angen, mae'n ddigonol rhoi rhestr dosraniadau rhwng-dyfodiad yn unig.
Am fwy o wybodaeth ar fewnbynnu dosraniadau, gwelwch :ref:`set-dists`.

Dangosir esiampl::

    Arrival_distributions={'Class 0': [['Exponential', 2.4],
                                       ['Uniform', 0.3, 0.5]],
                           'Class 1': [['Exponential', 3.0],
                                       ['Deterministic', 0.8]]}

Esiampl lle mae ond un dosbarth cwsmer::

    Arrival_distributions=[['Exponential', 2.4],
                           ['Exponential', 2.0]]


Baulking_functions
~~~~~~~~~~~~~~~~~~

*Opsiynol*

Geiriadur o ffwythiannau balcio ar gyfer pob dosbarth cwsmer a pob nod.
Mae'n disgrifio mecanweithiau balcio cwsmeriaid.
Am fwy o wybodaeth gwelwch :ref:`baulking-functions`.
Os hepgorwyd, yna ni balciwyd cwsmeriaid.

Esiampl::

    Baulking_functions={'Class 0': [probability_of_baulking]}



Class_change_matrices
~~~~~~~~~~~~~~~~~~~~~

*Opsiynol*

Geiriadur o fatricsau newid dosbarth ar gyfer pob nod.
Am fwy o wybodaeth gwelwch :ref:`dynamic-classes`.

Esiampl o rwydwaith dau nod gyda dau ddosbarth cwsmer::

    Class_change_matrices={'Node 0': [[0.3, 0.4, 0.3],
                                      [0.1, 0.9, 0.0],
                                      [0.5, 0.1, 0.4]],
                           'Node 1': [[1.0, 0.0, 0.0],
                                      [0.4, 0.5, 0.1],
                                      [0.2, 0.2, 0.6]]}


Number_of_servers
~~~~~~~~~~~~~~~~~

*Angenrheidiol*

Rhestr o nifer o weinyddion paralel wrth bob nod.
Os ddefnyddir amserlen gweinydd, rhowch yr amserlen yn lle rhif.
Am fwy o wybodaeth ar amserlenni gweinyddion, gwelwch :ref:`server-schedule`.
Ar gyfer nifer anfeidraidd o weinyddion gall rhoi 'Inf'.

Esiampl::

    Number_of_servers=[1, 2, 'Inf', 1, 'schedule']


Priority_classes
~~~~~~~~~~~~~~~~

*Opsiynol*

Geiriadur sy'n mapio dosbarthau cwsmer i flaenoriaethau.
Am fwy o wybodaeth, gwelwch :ref:`priority-custs`.
Os hepgorwyd, ni ddefnyddir blaenoriaeth, hynny yw mai gan bob cwsmer blaenoriaeth hafal.

Esiampl::

    Priority_classes={'Class 0': 0,
                      'CLass 1': 1,
                      'Class 2': 1}



Queue_capacities
~~~~~~~~~~~~~~~~

*Opsiynol*

Rhestr o gynhwysedd ciw macsimwm wrth bob nod.
Os hepgorwyd, y gwerthoedd diofyn yw 'Inf' ar gyfer pob nod.

Esiampl::

    Queue_capacities=[5, 'Inf', 'Inf', 10]


Service_distributions
~~~~~~~~~~~~~~~~~~~~~

*Angenrheidiol*

Mae'n disgrifio'r dosraniadau gwasanaeth ar gyfer pob nod a pob dosbarth cwsmer.
Geiriadur yw hwn gyda dosbarthiadau cwsmer fel allweddau, a rhestrau yn disgrifio dosraniadau gwasanaeth pob nod fel gwerthoedd.
Os ond un dosbarth cwsmer sydd angen, mae'n ddigonol rhoi rhestr dosraniadau rhwng-dyfodiad yn unig.
Am fwy o wybodaeth ar fewnbynnu dosraniadau, gwelwch :ref:`set-dists`.

Dangosir esiampl::

    Service_distributions={'Class 0': [['Exponential', 4.4],
                                       ['Uniform', 0.1, 0.9]],
                           'Class 1': [['Exponential', 6.0],
                                       ['Lognormal', 0.5, 0.6]]}

Esiampl lle mae ond un dosbarth cwsmer::

    Service_distributions=[['Exponential', 4.8],
                           ['Exponential', 5.2]]



Transition_matrices
~~~~~~~~~~~~~~~~~~~

*Angenrheidiol ar gyfer mwy nag un nod*

*Opsiynol ar gyfer un nod*

Mae'n disgrifio'r matrics trosglwyddo ar gyfer pob dosbarth cwsmer.
Geiriadur yw hwn gyda dosbarthiadau cwsmer fel allweddau, a rhestr o restrau (matricsau) yn cynnwys y tebygolrwyddau trosglwyddo fel gwerthoedd.
Os ond un dosbarth cwsmer sydd angen, mae'n ddigonol rhoi un matrics trosglwyddo yn unig (rhestr o restrau).

Dangosir esiampl::

    Transition_matrices={'Class 0': [[0.1, 0.3],
                                     [0.0, 0.8]],
                         'Class 1': [[0.0, 1.0],
                                     [0.0, 0.0]]}

Esiampl lle mae ond un dosbarth cwsmer::

    Transition_matrices=[[0.5, 0.3],
                         [0.2, 0.6]]

Os ddefnyddir un nod yn unig, y gwerth diofyn yw::

    Transition_matrices={'Class 0': [[0.0]]}