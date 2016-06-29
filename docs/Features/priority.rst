.. _priority-queues:

========================
Ciwiau Gyda Blaenoriaeth
========================

Mae gan Ciw'r gallu i aseinio blaenoriaethau i'r dosbarthiadau cwsmer. Gall gwneud hyn yn syml trwy fapio'r dosbarthiadau cwsmer i'r dosbarthiadau blaenoriaeth, wedi'i chynnwys yn y geiriadur paramedrau. Dangosir esiampl::

    >>> params = {
    ...     'Arrival_distributions': {'Class 0': [['Exponential', 2.0]],
    ...                               'Class 1': [['Exponential', 2.0]],
    ...                               'Class 2': [['Exponential', 1.0]]},
    ...     'Service_distributions': {'Class 0': [['Exponential', 5.0]],
    ...                               'Class 1': [['Exponential', 5.0]],
    ...                               'Class 2': [['Exponential', 4.0]]},
    ...     'Transition_matrices': {'Class 0': [[0.0]],
    ...                             'Class 1': [[0.0]],
    ...                             'Class 2': [[0.0]]},
    ...     'Number_of_servers': [1],
    ...     'Priority_classes': {'Class 0': 0,
    ...                          'CLass 1': 1,
    ...                          'Class 2': 1}
    ... }

Mae hwn yn dangos system M/M/1 gyda thri dosbarth cwsmer, wedi'i mapio i ddau ddosbarth blaenoriaeth. Mae gan gwsmeriaid yn nosbarth cwsmer 0 y flaenoriaeth uchaf wedi'i osod yn nosbarth blaenoriaeth 0. Mae cwsmeriaid yn nosbarth cwsmer 1 a 2 wedi'i osod yn nosbarth blaenoriaeth 1; mae ganddyn nhw'r un flaenoriaeth a'i gilydd, ond llai o flaenoriaeth na'r cwsmeriaid yn nosbarth 0.

Noder:

* Po leiaf yw'r dosbarth blaenoriaeth, po fwyaf y flaenoriaeth. Mae gan gwsmeriaid yn nosbarth blaenoriaeth 0 mwy o flaenoriaeth na'r cwsmeriaid yn nosbarth blaenoriaeth 1, sydd a fwy o flaenoriaeth na'r cwsmeriaid yn nosbarth blaenoriaeth 2, ayyb.
* Mae dosbarthiadau blaenoriaeth yn indecsau Python, felly os oes cyfanswm o 5 dosbarth blaenoriaeth, RHAID i'r dosbarthiadau blaenoriaeth cael ei labelu'n 0, 1, 2, 3, 4. Mae sgipio dosbarth blaenoriaeth, neu labelu'r dosbarthiadau yn unrhywbeth heblaw cyfanrifau cynyddol o 0 wedi'i wahardd.
* Y ddisgyblaeth blaenoriaeth a ddefnyddiwyd yw di-rhagymosodiadol. Mae cwsmeriaid yn gorffen ei wasanaeth ac nid ydynt yn cael ei thorri ar ei thraws gan gwsmeriaid gyda blaenoriaeth uwch.
