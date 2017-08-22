.. _tutorial-ii:

==============================================
Tiwtorial II: Archwilio'r Gwrthrych Simulation
==============================================

Yn y tiwtorial diwethaf, diffinion ac efelychon ni ein banc am ddiwrnod::

    >>> import ciw
    >>> N = ciw.create_network(
    ...     Arrival_distributions=[['Exponential', 0.2]],
    ...     Service_distributions=[['Exponential', 0.1]],
    ...     Number_of_servers=[3]
    ... )
    >>> ciw.seed(1)
    >>> Q = ciw.Simulation(N)
    >>> Q.simulate_until_max_time(1440)

Gadewch i ni archwilio'r gwrthrych Simulation :code:`Q`.
Er bod ein system ond yn cynnwys un nod (y banc), mae'r gwrthrych :code:`Q` wedi'i chreu o dri.
Gallwn mynedu'r nodau gan ddefnyddio::

    >>> Q.nodes
    [Arrival Node, Node 1, Exit Node]

+ **Y Nod Dyfodi (:code:`Arrival Node`):**
  Dyma le mae cwsmeriaid yn cael eu creu. Caiff ei silio yma, ac fe allant nhw :ref:`balcio <baulking-functions>`, :ref:`cael eu gwrthod <tutorial-vi>` neu gael eu hanfon i nod wasanaeth. Gallwn ei mynedu gan ddefnyddio::

    >>> Q.nodes[0]
    Arrival Node

+ **Nodau Wasanaeth:**
  Dyma le mae cwsmeriaid yn ciwio ac yn derbyn gwasanaeth. Gallwn feddwl am hwn fel y banc ei hun. Gallwn ei mynedu gan ddefnyddio::

    >>> Q.nodes[1]
    Node 1

+ **Yr Allanfa (:code:`Exit Node`):**
  Pan mae cwsmeriaid yn gadael y system, caiff eu casglu fan hyn. Yna, pan hoffwn ddarganfod beth ddigwyddodd yn ystod rhediad yr efelychiad, gallwn ffeindio'r cwsmeriaid yma. Gallwn ei mynedu gan ddefnyddio::

    >>> Q.nodes[-1]
    Exit Node

Unwaith bod yr efelychiad wedi rhedeg, mae'r gwrthrych Simulation yn aros yn yr union gyflwr a wnaeth e gyrraedd ar ddiwedd rhediad yr efelychiad.
Felly, mae’r gwrthrych Simulation ei hun yn gallu rhoi gwybodaeth ynglŷn â beth wnaeth digwydd yn ystod y rhediad.
Mae'r :code:`Exit Node` yn cynnwys holl gwsmeriaid gwnaeth gorffen gwasanaeth yn y banc, yn y drefn a wnaethon nhw adael y system::

    >>> Q.nodes[-1].all_individuals
    [Individual 2, Individual 3, Individual 5, ..., Individual 272]

Mae'r nod gwasanaeth hefyd yn cynnwys cwsmeriaid, rheina sydd dal yn aros neu yn derbyn gwasanaeth ar yr union amser gwnaeth rhediad yr efelychiad gorffen.
Yn y rhediad yma, roedd yna un cwsmer ar ôl yn y banc ar ddiwedd y dydd::

    >>> Q.nodes[1].all_individuals
    [Individual 274]

Gadewch i ni edrych ar yr unigolyn cyntaf i orffen gwasanaeth, :code:`Individual 2`.
Mae unigolion yn cario cofnodion data, sy'n cynnwys gwybodaeth fel dyddiad dyfodi, amser aros, a'r dyddiad gadael::

    >>> ind = Q.nodes[-1].all_individuals[0]
    >>> ind
    Individual 2
    >>> len(ind.data_records)
    1

    >>> ind.data_records[0].arrival_date
    7.936299...
    >>> ind.data_records[0].waiting_time
    0.0
    >>> ind.data_records[0].service_start_date
    7.936299...
    >>> ind.data_records[0].service_time
    2.944637...
    >>> ind.data_records[0].service_end_date
    10.88093...
    >>> ind.data_records[0].exit_date
    10.88093...

Nid yw hwn yn ffordd effeithlon o weld canlyniadau.
Yn y tiwtorial nesaf byddwn yn edrych i mewn i eneradu rhestrau o gofnodion i allu cael ystadegau cryno.