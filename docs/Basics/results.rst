.. _results-data:

===========
Canlyniadau
===========

Mae yna nifer o ffyrdd i cael gafael ar canlyniadau'r efelychiad:

- :ref:`sim_recs`
- :ref:`count_losses`
- :ref:`access_nodes`

Yn gyntaf, dweud fod gennym system blocio dau nod, a rhedwch am 1.5 uned amser:

    >>> import ciw
    
    >>> params = {
    ... 'Arrival_distributions': [['Exponential', 6.0],
    ...                           ['Exponential', 2.5]],
    ... 'Service_distributions': [['Exponential', 8.5],
    ...                           ['Exponential', 5.5]],
    ... 'Transition_matrices': [[0.0, 1.0],
    ...                         [0.0, 0.0]],
    ... 'Number_of_servers': [2, 1],
    ... 'Queue_capacities': [3, 4]
    ... }

    >>> ciw.seed(10)
    >>> N = ciw.create_network(params)
    >>> Q = ciw.Simulation(N)
    >>> Q.simulate_until_max_time(1.5)

.. _sim_recs:

-----------------------
Cofnodion yr Efelychiad
-----------------------

Pob tro mae unigolyn yn cyflawni gwasanaeth yn orsaf gwasanaeth, mae cofnod data o'r gwasanaeth hwnna yn cael ei chadw. Dylai'r cofnodion edrych fel y tabl isod:

    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-------------+-----------------------+-------------------------+
    | I.D number | Class | Node | Arrival Date | Waiting Time | Service Start Date | Service Time | Service End Date | Time Blocked | Exit Date | Destination | Queue Size at Arrival | Queue Size at Departure |
    +============+=======+======+==============+==============+====================+==============+==================+==============+===========+=============+=======================+=========================+
    | 227592     | 1     | 1    | 245.601      | 0.0          | 245.601            | 0.563        | 246.164          | 0.0          | 246.164   | -1          | 0                     | 2                       |
    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-------------+-----------------------+-------------------------+
    | 411239     | 0     | 1    | 245.633      | 0.531        | 246.164            | 0.608        | 246.772          | 0.0          | 246.772   | -1          | 1                     | 5                       |
    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-------------+-----------------------+-------------------------+
    | 001195     | 0     | 2    | 247.821      | 0.0          | 247.841            | 1.310        | 249.151          | 0.882        | 250.033   | 1           | 0                     | 0                       |
    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-------------+-----------------------+-------------------------+
    | ...        | ...   | ...  | ...          | ...          | ...                | ...          | ...              | ...          | ...       | ...         | ...                   | ...                     |
    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-------------+-----------------------+-------------------------+

Fe allwch cael mynediad i'r cofnodion yma fel rhestr o `named tuples', yn defnyddio method y gwrthrych Simulation :code:`get_all_records`:

    >>> recs = Q.get_all_records()

Mae gan y cofnodion data yr enwau newidynnau canlynol:

    - :code:`id_number`
    - :code:`customer_class`
    - :code:`node`
    - :code:`arrival_date`
    - :code:`waiting_time`
    - :code:`service_start_date`
    - :code:`service_time`
    - :code:`service_end_date`
    - :code:`time_blocked`
    - :code:`exit_date`
    - :code:`destination`
    - :code:`queue_size_at_arrival`
    - :code:`queue_size_at_departure`

O fan hyn, fe allwn cael edrych ar nifer o mesuron perfformiad trwy trin y rhestr yma. Er enghraifft, i ddadansoddi'r amserau aros a ddigwyddodd yn Nod 2:

    >>> waits2 = [r.waiting_time for r in recs if r.node == 2]
    >>> waits2
    [0.0, 0.17402..., 0.25654..., 0.245544...]
    >>> sum(waits2) / len(waits2)
    0.16902829492661808

Efallai hoffwch weld amseroedd gwasanaeth pob cwsmer a pasiodd trwy Nod 1:

    >>> service1 = [r.service_time for r in recs if r.node == 1]
    >>> service1
    [0.05654..., 0.13221..., 0.127559..., 0.10152..., 0.19745...]


.. _count_losses:

---------------
Cyfri Colledion
---------------

Fe fydd nodau gyda cynhwysedd ciwio cyfyngedig yn gwrthod cwsmeriaid newydd sy'n cyrraedd os ydynt yn cyraedd pan mae'r nod yn llawn. Mae'r colledion yma yn cael eu recordio mewn :code:`rejection_dict`. Dyma geiriadur o geiriaduron, gyda nodau a dosbarthau cwsmer fel allweddau, a rhestr o dyddiadau cyrraedd fel gwerthoedd.

    >>> Q.rejection_dict
    {1: {0: []}, 2: {0: [0.79694..., 1.17701..., 1.19512..., 1.25265...]}}

Fan hyn welwn fod colled cwsmer o dosbarth cwsmer 0 yn Nod 2 ar dyddiadau 0.796, 1.770, 1.195, a 1.252.
Os hoffwn weld nifer of colledion dosbarth cwsmer 0 yn Nod 2:

    >>> number_of_losses_class0_node2 = len(Q.rejection_dict[2][0])
    >>> number_of_losses_class0_node2
    4

I weld cyfanswm nifer o colledion, rhaid swmio dros holl nodau a dosbarth cwsmer:

    >>> number_of_losses = sum(
    ...     [len(Q.rejection_dict[nd][cls]) for nd in
    ...     range(1, N.number_of_nodes + 1) for cls in
    ...     range(N.number_of_classes)])
    >>> number_of_losses
    4


.. _access_nodes:

-----------------------
Cael Mynediad i'r Nodau
-----------------------

Ar ôl i'r efelychiad gorffen, mae'r gwrthrych Simulation :code:`Q` yn aros yn yr union un cylwr yr oedd ar diwedd yr efelychiad. Felly mae pob nod dal yn cynnwys unrhyw cwsmeriaid a oedd yn aros neu'n cael gwasanaeth yn y nod yna ar diwedd yr efelychiad. Fe all hwn fod yn ddadlennol, yn enwedig yr Exit Node.

Yn gyntaf, edrychwn ar y nodau eu hun:

    >>> Q.nodes
    [Arrival Node, Node 1, Node 2, Exit Node]

Mae'r Exit Node yn cynnwys holl unigolion sydd wedi gadael y system:

    >>> Q.nodes[-1].all_individuals
    [Individual 3, Individual 1, Individual 4, Individual 2]

Mae hwn yn dweud wrthon fod 4 unigolyn wedi gorffen eu gwasanaethau ac wedi gadael y system. Fe allwn hefyd edrych ar yr unigolion sydd dal yn y nodau wasanaeth:

    >>> Q.nodes[1].all_individuals
    [Individual 10, Individual 15, Individual 16, Individual 17]
    
    >>> Q.nodes[2].all_individuals
    [Individual 5, Individual 6, Individual 7, Individual 8, Individual 9]

Wrth cyfuno'r wybodaeth hwn gyda'r wybodaeth a cawsom o'r :code:`rejection_dict`, rydym nawr yn gwybod pob unigolyn aeth i mewn i'r system:

- Fe wnaeth Unigolion 1 i 4 cwblhau bod gwasanaeth.
- Fe wnaeth Unigolion 5 i 9 cyrraedd Nod 2, ond aethen nhw ddim pellach.
- Fe wnaeth Unigolyn 10, a 15 i 17 cyrraedd Nod 1, ond aethen nhw ddim pellach.
- Roedd 4 Unigolyn wedi'i wrthod, ac felly Unigolion 11 i 14 cafodd eu wrthod.
