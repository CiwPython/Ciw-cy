.. _server-schedule:

=================================
Sut i Osod Amserlenni Gweinyddion
=================================

Gyda Ciw fe allwch aseinio amserlenni gwaith cylchol i'r gweinyddion ym mhob gorsaf gwasanaeth.
Dangosir amserlen gwaith cylchol enghreifftiol yn y tabl isod:

    +--------------------+--------+--------+--------+
    |     Amser Sifft    |   0-10 |  10-30 | 30-100 |
    +--------------------+--------+--------+--------+
    | Nifer o Weinyddion |      2 |      0 |      1 |
    +--------------------+--------+--------+--------+

Mae'r amserlen yn gylchol, yna ar ôl y sifft olaf (30-100), mae'r amserlen yn dechrau eto gyda'r sifft (0-10).
Hyd y cylchred ar gyfer yr amserlen yma yw 100.
Diffinnir hwn gan restr o restrau yn dynodi nifer o weinyddion dylai fod ar ddyletswydd yn ystod y sifft yna, a dyddiad diwedd y sifft::

    [[2, 10], [0, 30], [1, 100]]

Fan hyn dywedwn ni fe fydd 2 gweinydd ar ddyletswydd rhwng amseroedd 0 a 10, 0 rhwng 10 a 30, ayyb.
Mae hwn yn diffinio'r amserlen gwaith cylchol yn llawn.

I ddweud wrth Ciw am ddefnyddio'r amserlen yma ar gyfer nod penodol, yn :code:`Number_of_servers` amnewidiwch y cyfanrif gyda'r amserlen::

    >>> import ciw
    >>> N = ciw.create_network(
    ...     Arrival_distributions=[['Exponential', 5]],
    ...     Service_distributions=[['Exponential', 10]],
    ...     Number_of_servers=[[[2, 10], [0, 30], [1, 100]]]
    ... )

Ar ôl efelychu'r system, gwelwn nad oes unrhyw wasanaethau yn dechrau rhwng dyddiadau 10 a 30, na rhwng dyddiadau 110 a 130::

    >>> ciw.seed(1)
    >>> Q = ciw.Simulation(N)
    >>> Q.simulate_until_max_time(205.0)
    >>> recs = Q.get_all_records()
    
    >>> [r for r in recs if 10 < r.service_start_date < 30]
    []
    >>> [r for r in recs if 110 < r.service_start_date < 130]
    []

**Nodwch ar hyn o bryd mae amserlenni gwaith yn anghydnaws gyda nifer anfeidraidd o weinyddion**, ac felly ni all amserlen cynnwys nifer anfeidraidd o weinyddion.



Rhagdarfiadau
-------------

Pan mae gweinydd angen mynd oddi ar ddyletswydd yng nghanol gwasanaeth cwsmer, mae yna dau opsiwn o beth gall ddigwydd.

+ Yn ystod amserlen rhagdarfiedig, fe fydd gweinydd yn stopio ar unwaith ac yn gadael. Pan mae gweinyddion newydd yn dod ar ddyletswydd fe fydden nhw’n blaenoriaethu’r cwsmeriaid a gafodd ei darfu. Ond mae amser gwasanaeth y cwsmeriaid yma yn cael ei ail-samplu.

+ Yn ystod amserlen anrhagdarfiedig, nid yw gwasanaethau cwsmeriaid yn cael ei darfu. Felly, mae gweinydd yn gorffen gwasanaeth y cwsmer presennol cyn diflannu. Mae hwn wrth gwrs yn golygu, pan mae gweinyddion newydd yn cyrraedd, efallai bydd yr hen weinyddion dal yna yn gorffen gwasanaeth y cwsmeriaid gwreiddiol.

Er mwyn gweithredu amserlennu rhagdarfiedig neu anrhagdarfiedig, rhaid rhoi’r amserlen mewn tuple, gyda :code:`True` neu :code:`False` fel yr ail derm, yn dynodi tarfiadau rhagdarfiedig neu anrhagdarfiedig.
Er enghraifft:

    Number_of_servers=[([[2, 10], [0, 30], [1, 100]], True)] # rhagdarfiedig

Ac::

    Number_of_servers=[([[2, 10], [0, 30], [1, 100]], False)] # anrhagdarfiedig

Mae Ciw yn defnyddio amserlennu anrhagdarfiedig fel yr opsiwn diofyn, felly mae’r cod isod yn awgrymu amserlen anrhagdarfiedig:

    Number_of_servers=[[[2, 10], [0, 30], [1, 100]]] # anrhagdarfiedig
