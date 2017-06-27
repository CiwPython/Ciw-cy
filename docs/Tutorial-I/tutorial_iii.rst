.. _tutorial-iii:

=================================
Tiwtorial III: Casglu Canlyniadau
=================================

Yn y tiwtorialau dwethaf gwnaethon ni diffinio ac efelychu banc am diwrnod, a gwelon ni sut i mynedu rhannau o'r injan efelychu::

    >>> import ciw
    >>> N = ciw.create_network(
    ...     Arrival_distributions=[['Exponential', 0.2]],
    ...     Service_distributions=[['Exponential', 0.1]],
    ...     Number_of_servers=[3]
    ... )
    >>> ciw.seed(1)
    >>> Q = ciw.Simulation(N)
    >>> Q.simulate_until_max_time(1440)

Yn gloi, gallwn ni cael rhestr o'r holl confnodion data a casglwyd gan holl cwsmeriaida gorffenodd o leia un gwasanaeth, gan ddefnyddio'r method :code:`get_all_records` o'r gwrthrych Simulation::

    >>> recs = Q.get_all_records()

Mae hwn yn rhoi rhestr o yuples enwedig.
Mae pob tuple yn cynnwys y gwybodaeth canlynol:

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

Roddir mwy o wybodaeth ar pob un o rhain yn :ref:`refs-results`.

Gan defnyddio list comprehension, gallwn ni cael rhestrau o pa bynnag ystadegyn a hoffwn::

    >>> # Rhestr o ameroedd wasanaeth
    >>> servicetimes = [r.service_time for r in recs]
    >>> servicetimes
    [2.94463..., 5.96912..., 0.28757..., ..., 10.46244...]

    >>> # Rhestr o'r amseroedd aros
    >>> waits = [r.waiting_time for r in recs]
    >>> waits
    [0.0, 0.0, 0.20439..., ..., 5.63781...]

Nawr fe allwn cael ystadegau cryno trwy trin y rhestrau yma::

    >>> mean_service_time = sum(servicetimes) / len(servicetimes)
    >>> mean_service_time
    9.543928...

    >>> mean_waiting_time = sum(waits) / len(waits)
    >>> mean_waiting_time
    1.688541...

Rydym nawr yn gwbod y amser aros cymedrig y cwsmeriaid!
Yn y tiwtorial nesaf fe fyddwn yn dangos sut i cael canlyniadau mwy cynrychioliadol (oherwydd fe efelychon ni am un diwrnod penodol yn unig fan hyn).

Gan defnyddio llyfrgelloedd arall gallwn derbyn ystadegau cryno pellach.
Rydyn ni yn awrymu `numpy <http://www.numpy.org/>`_, `pandas <http://pandas.pydata.org/>`_ a `matplotlib <http://matplotlib.org/>`_. 
Mae rhain yn rhoi'r gallu i archwilio ystadegau arall, a plotio.
Crëwyd y histogram o ameroess aros isod gan defnyddio matplotlib, yn defnyddio'r cod canlynol::

    >>> import matplotlib.pyplot as plt # doctest:+SKIP
    >>> plt.hist(waits); # doctest:+SKIP

.. image:: ../_static/tutorial_iii_waitshist.svg
   :scale: 100 %
   :alt: Histogram o amseroedd aros ar gyfer Tiwtorial III.
   :align: center

Yn y tiwtorial nesaf dangoswn ni sut i defnyddio Ciw i cael canlyniadau dibynadwy, ac o'r diwedd ffeindio'r amser aros cymedrig ar gyfer y banc.