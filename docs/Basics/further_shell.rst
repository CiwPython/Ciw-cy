Yn Ddyfnach
===========

Yn :ref:`getting-started` fe welwch sut i redeg efelychiad syml. Mae'r tudalen hwn yn gadael i chi cyrchu'r efelychiad trwy archwilio'r cod mewnol
Yn gyntaf, sefydlwch y ffeil paramedrau fel y disgrifiwyd yn :ref:`parameters-file`.

Nawr mae llwytho Ciw a'r ffeil paramedrau fel geiriadur yn syml::

    >>> import ciw
    >>> params = ciw.load_parameters(<path_i_ffeil>) # doctest:+SKIP
    >>> params["Number_of_servers"] # doctest:+SKIP
    [2, 1, 1] # doctest:+SKIP

Sefydlwch wrthrych Simulation, lle allwch gael mynediad i'r paramedrau::

    >>> Q = ciw.Simulation(params) # doctest:+SKIP
    >>> Q.number_of_nodes # doctest:+SKIP
    3 # doctest:+SKIP
    >>> Q.queue_capacities # doctest:+SKIP
    ['Inf', 'Inf', 10] # doctest:+SKIP
    >>> Q.lmbda    # Dosraniadau dyfodiad i'r system # doctest:+SKIP
    [[['Exponential', 1.0], ['Exponential', 1.8], ['Exponential', 7.25]], [['Exponential', 6.0], ['Exponential', 4.5], ['Exponential', 2.0]]] # doctest:+SKIP
    >>> Q.lmbda[0]    # Dosraniadau dyfodiad y 0eg dosbarth cwsmer # doctest:+SKIP
    [['Exponential', 1.0], ['Exponential', 1.8], ['Exponential', 7.2]] # doctest:+SKIP

Fe allwch ffeindio rhestr lawn o wrthrychau a phriodweddau Ciw fan hyn: :ref:`objects-attributes`.
Nawr i redeg efelychiad, redwch y method canlynol::

    >>> Q.simulate_until_max_time() # doctest:+SKIP

Medrwch cael mynediad i recordiau data'r unigolion trwy'r methodau canlynol::

    >>> all_individuals = Q.get_all_individuals()    # Creu rhestr holl cwsmeriaid yn y system # doctest:+SKIP
    >>> all_individuals[0] # doctest:+SKIP
    Individual 13 # doctest:+SKIP
    >>> all_individuals[0].data_records.values()[0][0].wait    # Yr amser oedd Unigolyn 13 yn aros ar gyfer yr achos hyn o wasanaeth # doctest:+SKIP
    0.39586652218275364 # doctest:+SKIP
    >>> all_individuals[0].data_records.values()[0][0].arrival_date # Amser cyrraedd Unigolyn 13 ar gyfer yr achos hyn o wasanaeth # doctest:+SKIP
    0.5736475797750542 # doctest:+SKIP

Fe allwch gael rhestr lawn y recordiau data, gyda neu heb bennawd::
    
    >>> records = Q.get_all_records(headers=True) # doctest:+SKIP
    >>> records[:3] # doctest:+SKIP
    [['I.D. Number', 'Customer Class', 'Node', 'Arrival Date', 'Waiting Time', 'Service Start Date', 'Service Time', 'Service End Date', 'Time Blocked', 'Exit Date'], # doctest:+SKIP
    [1, 0, 1, 0.16207509531905792, 0.0, 0.16207509531905792, 0.014861757967438763, 0.1769368532864967, 0.0, 0.1769368532864967], # doctest:+SKIP
    [2, 0, 1, 0.4628182409609607, 0.0, 0.4628182409609607, 0.13420139243827206, 0.5970196333992328, 0.0, 0.5970196333992328]] # doctest:+SKIP

Gall ysgrifennu'r rhestr lawn o recordiau data i ffeil csv::

    >>> Q.write_records_to_file(<path_i_ffeil>) # doctest:+SKIP

Gwelwch :ref:`output-file` ar gyfer esboniad llawn o'r data hwn.