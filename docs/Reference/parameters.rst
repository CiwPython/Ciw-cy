.. _refs-params:

=================
Rhestr Paramedrau
=================

Isod rhestrwyd holl baramedrau mae'r ffwythiant :code:`create_network` yn cymryd, ynghyd â disgrifiadau o'r gwerthoedd a chymerwyd.
Os ddefnyddir ffeil paramedrau, yna dyma ddadleuon a gwerthoedd sydd angen yn y ffeil :code:`.yml`.


arrival_distributions
~~~~~~~~~~~~~~~~~~~~~

*Angenrheidiol*

Mae'n disgrifio'r dosraniadau rhwng-dyfodiad ar gyfer pob nod a pob dosbarth cwsmer.
Geiriadur yw hwn gyda dosbarthiadau cwsmer fel allweddau, a rhestrau yn disgrifio dosraniadau rhwng-dyfodiad pob nod fel gwerthoedd.
Os ond un dosbarth cwsmer sydd angen, mae'n ddigonol rhoi rhestr dosraniadau rhwng-dyfodiad yn unig.
Am fwy o wybodaeth ar fewnbynnu dosraniadau, gwelwch :ref:`set-dists`.

Dangosir esiampl::

    arrival_distributions={'Class 0': [ciw.dists.Exponential(2.4),
                                       ciw.dists.Uniform(0.3, 0.5)],
                           'Class 1': [ciw.dists.Exponential(3.0),
                                       ciw.dists.Deterministic(0.8)]}

Esiampl lle mae ond un dosbarth cwsmer::

    arrival_distributions=[ciw.dists.Exponential(2.4),
                           ciw.dists.Exponential(2.0)]


batching_distributions
~~~~~~~~~~~~~~~~~~~~~~

*Opsiynol*

Mae hwn yn disgrifio dosraniadau maint y swp-dyfodiadau ar gyfer pob nod a dosbarth cwsmer.
Geiriadur yw hwn gyda dosbarthiadau cwsmer fel allweddau, a rhestrau yn disgrifio dosraniadau swp-dyfodiad pob nod fel gwerthoedd.
Os ond un dosbarth cwsmer sydd angen, mae'n ddigonol rhoi rhestr dosraniadau swp-dyfodiad yn unig.
Am fwy o wybodaeth ar swp-dyfodiadau, gwelwch :ref:`batch-arrivals`.

Dangosir esiampl::

    batching_distributions={'Class 0': [ciw.dists.Deterministic(1),
                                        ciw.dists.Sequential([1, 1, 2])],
                            'Class 1': [ciw.dists.Deterministic(3),
                                        ciw.dists.Deterministic(2)]}

Esiampl lle mae ond un dosbarth cwsmer::

    batching_distributions=[ciw.dists.Deterministic(2),
                            ciw.dists.Deterministic(1)]



baulking_functions
~~~~~~~~~~~~~~~~~~

*Opsiynol*

Geiriadur o ffwythiannau balcio ar gyfer pob dosbarth cwsmer a pob nod.
Mae'n disgrifio mecanweithiau balcio cwsmeriaid.
Am fwy o wybodaeth gwelwch :ref:`baulking-functions`.
Os hepgorwyd, yna ni balciwyd cwsmeriaid.

Esiampl::

    baulking_functions={'Class 0': [probability_of_baulking]}



xlass_change_matrices
~~~~~~~~~~~~~~~~~~~~~

*Opsiynol*

Geiriadur o fatricsau newid dosbarth ar gyfer pob nod.
Am fwy o wybodaeth gwelwch :ref:`dynamic-classes`.

Esiampl o rwydwaith dau nod gyda dau ddosbarth cwsmer::

    class_change_matrices={'Node 0': [[0.3, 0.4, 0.3],
                                      [0.1, 0.9, 0.0],
                                      [0.5, 0.1, 0.4]],
                           'Node 1': [[1.0, 0.0, 0.0],
                                      [0.4, 0.5, 0.1],
                                      [0.2, 0.2, 0.6]]}


number_of_servers
~~~~~~~~~~~~~~~~~

*Angenrheidiol*

Rhestr o nifer o weinyddion paralel wrth bob nod.
Os ddefnyddir amserlen gweinydd, rhowch yr amserlen yn lle rhif.
Am fwy o wybodaeth ar amserlenni gweinyddion, gwelwch :ref:`server-schedule`.
Ar gyfer nifer anfeidraidd o weinyddion gall rhoi :code;`float('inf')`.

Esiampl::

    number_of_servers=[1, 2, float('inf'), 1, 'schedule']


priority_classes
~~~~~~~~~~~~~~~~

*Opsiynol*

Geiriadur sy'n mapio dosbarthau cwsmer i flaenoriaethau.
Am fwy o wybodaeth, gwelwch :ref:`priority-custs`.
Os hepgorwyd, ni ddefnyddir blaenoriaeth, hynny yw mai gan bob cwsmer blaenoriaeth hafal.

Esiampl::

    priority_classes={'Class 0': 0,
                      'CLass 1': 1,
                      'Class 2': 1}



Queue_capacities
~~~~~~~~~~~~~~~~

*Opsiynol*

Rhestr o gynhwysedd ciw macsimwm wrth bob nod.
Os hepgorwyd, y gwerthoedd diofyn yw :code:`float('inf')` ar gyfer pob nod.

Esiampl::

    queue_capacities=[5, float('inf'), float('inf'), 10]


routing
~~~~~~~

*Angenrheidiol ar gyfer mwy nag un nod*

*Opsiynol ar gyfer un nod*

Mae'n disgrifio'r ffordd y mae pob dosbarth cwsmer yn teithio o gwmpas y system.
Gall hyn fod yn matrics trosglwyddo ar gyfer pob dosbarth cwsmer, neu ffwythiant teithio ar gyfer efelychiadau wedi'u weilio ar brosesau, gweler :ref:`process-based`.

Geiriadur yw hwn gyda dosbarthiadau cwsmer fel allweddau, a rhestr o restrau (matricsau) yn cynnwys y tebygolrwyddau trosglwyddo fel gwerthoedd.
Os ond un dosbarth cwsmer sydd angen, mae'n ddigonol rhoi un matrics trosglwyddo yn unig (rhestr o restrau).

Dangosir esiampl::

    routing={'Class 0': [[0.1, 0.3],
                         [0.0, 0.8]],
             'Class 1': [[0.0, 1.0],
                         [0.0, 0.0]]}

Esiampl lle mae ond un dosbarth cwsmer::

    routing=[[0.5, 0.3],
             [0.2, 0.6]]

Os ddefnyddir un nod yn unig, y gwerth diofyn yw::

    routing={'Class 0': [[0.0]]}

Fel arall defnyddiwch ffwythiant teithio::

    routing=[routing_function]




service_distributions
~~~~~~~~~~~~~~~~~~~~~

*Angenrheidiol*

Mae'n disgrifio'r dosraniadau gwasanaeth ar gyfer pob nod a pob dosbarth cwsmer.
Geiriadur yw hwn gyda dosbarthiadau cwsmer fel allweddau, a rhestrau yn disgrifio dosraniadau gwasanaeth pob nod fel gwerthoedd.
Os ond un dosbarth cwsmer sydd angen, mae'n ddigonol rhoi rhestr dosraniadau rhwng-dyfodiad yn unig.
Am fwy o wybodaeth ar fewnbynnu dosraniadau, gwelwch :ref:`set-dists`.

Dangosir esiampl::

    service_distributions={'Class 0': [ciw.dists.Exponential(4.4),
                                       ciw.dists.Uniform(0.1, 0.9)],
                           'Class 1': [ciw.dists.Exponential(6.0),
                                       ciw.dists.Lognormal(0.5, 0.6)]}

Esiampl lle mae ond un dosbarth cwsmer::

    service_distributions=[ciw.dists.Exponential(4.8),
                           ciw.dists.Exponential(5.2)]
