.. _exact-arithmetic:

================================
Sut i Ddefnyddio Rhifyddeg Union
================================

Oherwydd y `problemau a chyfyngiadau <https://docs.python.org/2/tutorial/floatingpoint.html>`_ sy'n codi wrth delio gyda rhifau pwynt arnawf, mae Ciw yn cynnig opsiwn rhifyddef union.
Cymerwch ofal, fodd bynnag, mae defnyddio hwn yn effeithio cyflymder, ac felly dylai ond cael ei ddefnyddio os yw problemau rhifyddeg arnawf yn effeithio eith canlyniadau.
Gall hwn ddigwydd, er enghraifft, wrth gyfuno defnydd dosraniadau penderfynedig ac amserlenni gweinyddion.

I weithredu rhifyddeg union, ychwanegwch y ddadl ganlynol wrth greu gwrthrych Simulation::

    >>> Q = ciw.Simulation(N, exact=26) # doctest:+SKIP

Mae'r ddadl :code:`exact` yn dynodi'r lefel trachywiredd.

Edrychwn ar esiampl::
    
    >>> import ciw
    >>> N = ciw.create_network(
    ...     Arrival_distributions=[['Exponential', 5]],
    ...     Service_distributions=[['Exponential', 10]],
    ...     Number_of_servers=[1]
    ... )

Heb ddefnyddio rhifyddeg union, gwelwn defnyddir rhifau pwynt arnawf trwy gydol y rhediad::

    >>> ciw.seed(2)
    >>> Q = ciw.Simulation(N)
    >>> Q.simulate_until_max_time(100.0)
    >>> waits = [r.waiting_time for r in Q.get_all_records()]
    >>> waits[-1]
    0.202518877171...
    >>> type(waits[-1])
    <class 'float'>

Os ddefnyddiwn rifyddeg union, defnyddir mathau :code:`decimal.Decimal` trwy gydol y rhediad::

    >>> ciw.seed(2)
    >>> Q = ciw.Simulation(N, exact=26)
    >>> Q.simulate_until_max_time(100.0)
    >>> waits = [r.waiting_time for r in Q.get_all_records()]
    >>> waits[-1]
    Decimal('0.2025188771714382860')
    >>> type(waits[-1])
    <class 'decimal.Decimal'>