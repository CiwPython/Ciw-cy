.. _priority-custs:

=========================
Sut i Osod Blaenoriaethau
=========================

Gall Ciw aseinio blaenoriaethau i dosbarthau cwsmer.
I wenud hwn rydym yn mapio dosbarthau cwsmer i dosbarthau blaenoriaeth, gan ychwanegu hwn fel allweddair wrth creu gwrthrych Network.
Dangosir enghraifft::

    Priority_classes={'Class 0': 0,
                      'Class 1': 1,
                      'Class 2': 1}

Mae hwn yn dangos mapiad o tri dosbarth cwsmer i dau dosbarth blaenoriaeth.
Mae gan cwsmeriaid dosbarth 0 y flaenoriaeth mwyaf, a'i rhoddir yn nosbarth blaenoriaeth 0.
Rhoddir cwsmeriaid dosbarth 1 a 2 yn dosbarth blaenoriaeth 1; mae ganddynt yr un flaenoriaeth a'i gilydd, ond llai o flaenoriaeth na cwsmeriaid dosbarth 0.

Nodwch:

* Po leifaf yw rhif y dosbarth blaenoriaeth, po fwyad yw'r blaenoriaeth. Mae gan cwsmeriaid yn nosbarth blaenoriaeth 0 mwy o flaenoriaeth na cwsmeriaid yn nosbarth blaenoriaeth 1, sydd a fwy o flaenoriaieth na cwsmeriaid yn nosbarth blaenoriaeth 2, ayyb.
* Indecsiau Python yw dosbarthau blaenoriaeth, felly os oes 5 dosbarth blaenoriaeth **rhaid** eu labelu 0, 1, 2, 3, 4. Fe fydd hepgor rhif, new enwi dosbarthau blaenoriaeth unrhywbeth arall heblaw cyfanrifau cynyddol o 0, yn achosu gwall.
* Mae disgybliaeth blaenoriaeth yn anrhagdarfiedig. Mae cwsmeriaid pob amser yn gorffen eu wasanaeth a nid yw'n cael eu darfu gan cwsmeriaid gyda blaenoriaeth uwch.

I weithredu hwn, crëwch gwrthrych Network gan ychwanegu'r allweddair :code:`Priority_classes` gyda'r mapiad::

    >>> import ciw
    >>> N = ciw.create_network(
    ...     Arrival_distributions={'Class 0': [['Exponential', 5]],
    ...                            'Class 1': [['Exponential', 5]]},
    ...     Service_distributions={'Class 0': [['Exponential', 10]],
    ...                            'Class 1': [['Exponential', 10]]},
    ...     Priority_classes={'Class 0': 0, 'Class 1': 1},
    ...     Number_of_servers=[1]
    ... )

Rhedwn yr efelychiad, yn cymharu'r amseroedd aros cwsmeriaid dosbarth 0 a dosbarth 1.
Dylai cwsmeriaid gyda mwy o flaenoriaeth cael amser aros cymedrig llai na'r cwsmeriaid gyda llai o flaenoriaeth::

    >>> ciw.seed(1)
    >>> Q = ciw.Simulation(N)
    >>> Q.simulate_until_max_time(100.0)
    >>> recs = Q.get_all_records()

    >>> waits_0 = [r.waiting_time for r in recs if r.customer_class==0]
    >>> sum(waits_0)/len(waits_0)
    0.1529189...

    >>> waits_1 = [r.waiting_time for r in recs if r.customer_class==1]
    >>> sum(waits_1)/len(waits_1)
    3.5065047...