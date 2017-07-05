.. _set-dists:

==========================================
Sut i Osod Dosraniadau Dyfodi a Gwasanaeth
==========================================

Mae Ciw yn cynnig amrywiaeth o ddosraniadau amser rhwng-dyfodiad a gwasanaeth.
Ffeindiwch restr lawn :ref:`fan hyn <refs-dists>`.
Diffinnir wrth greu gwrthrych Network gyda'r allweddeiriau :code:`'Arrival_distributions'` a :code:`'Service_distributions'`.

+ :code:`'Arrival_distributions'`: Dyma'r dosraniad a samplwyd amseroedd rhwng-dyfodiad. Hynny yw yr amser rhwng dau ddyfodiad olynol. Mae'n benodol ar gyfer nodau a dosbarthau cwsmer spesifig.
+ :code:`'Service_distributions'`: Dyma'r dosraniad a samplwyd amseroedd gwasanaeth. Hynny yw faint o amser mae cwsmer yn gwario gyda gweinydd (yn annibynnol o faint o weinyddion sydd yno). Mae'n benodol ar gyfer nodau a dosbarthau cwsmer spesifig.

Mae'r enghraifft ganlynol, gyda dau nod a dau ddosbarth cwsmer, y defnyddio wyth gwahanol ddosraniad dyfodi a gwasanaeth::

    >>> import ciw
    >>> N = ciw.create_network(
    ...     Arrival_distributions={'Class 0': [['Deterministic', 0.4],
    ...                                        ['Empirical', [0.1, 0.1, 0.1, 0.2]]],
    ...                            'Class 1': [['Deterministic', 0.2],
    ...                                        ['Custom', [0.2, 0.4], [0.5, 0.5]]]},
    ...     Service_distributions={'Class 0': [['Exponential', 6.0],
    ...                                        ['Lognormal', -1, 0.5]],
    ...                            'Class 1': [['Uniform', 0.1, 0.7],
    ...                                        ['Triangular', 0.2, 0.7, 0.3]]},
    ...     Transition_matrices={'Class 0': [[0.0, 0.0], [0.0, 0.0]],
    ...                          'Class 1': [[0.0, 0.0], [0.0, 0.0]]},
    ...     Number_of_servers=[1, 1]
    ... )


Rhedwn hwn (gyda :ref:`rhifyddeg union <exact-arithmetic>`) am 25 uned amser::

    >>> ciw.seed(10)
    >>> Q = ciw.Simulation(N, exact=10)
    >>> Q.simulate_until_max_time(50)
    >>> recs = Q.get_all_records()

Mae'r system yn defnyddio'r wyth dosraniad canlynol:

+ :code:`['Deterministic', 0.4]`:
   + Samplu 0.4 pob amser.
+ :code:`['Deterministic', 0.2]`:
   + Samplu 0.2 pob amser.
+ :code:`['Empirical', [0.1, 0.1, 0.1, 0.2]`:
   + Samplu'r rhifau 0.1, 0.1, 0.1 a 0.2 ar hap.
+ :code:`['Custom', [[0.5, 0.2], [0.5, 0.4]]]`:
   + Samplu 0.2 hanner yr amser, a 0.4 hanner yr amser.
+ :code:`['Exponential', 6.0]`:
   + Samplu o'r dosraniad `esbonyddol <https://en.wikipedia.org/wiki/Exponential_distribution>`_ gyda paramedr :math:`\lambda = 6.0`. Cymedr disgwyliedig o 0.1666...
+ :code:`['Uniform', 0.1, 0.7]`:
   + Samplu unrhyw rhif rhwng 0.1 a 0.7 gyda tebygolrwydd hafal. Cymedr disgwyliedig o 0.4.
+ :code:`['Lognormal', -1, 0.5]`:
   + Samplu o;r dosraniad `lognormal <https://en.wikipedia.org/wiki/Log-normal_distribution>`_ gyda paramedrau :math:`\mu = -1` a :math:`\sigma = 0.5`. Cymedr disgwyliedig o 0.4724...
+ :code:`['Triangular', 0.2, 0.7, 0.3]`:
   + Samplu o'r dosraniad `trionglog <https://en.wikipedia.org/wiki/Triangular_distribution>`_ gyda modd 0.3, terfyn isaf 0.2 a terfyn uchaf 0.7. Cymedr disgwyliedig o 0.4.

O'r holl gofnodion data, casglwch yr amseroedd gwasanaeth a'r dyddiadau dyfodi ar gyfer pob nod a pob dosbarth cwsmer::

    >>> servicetimes_n1c0 = [r.service_time for r in recs if r.node==1 and r.customer_class==0]
    >>> servicetimes_n2c0 = [r.service_time for r in recs if r.node==2 and r.customer_class==0]
    >>> servicetimes_n1c1 = [r.service_time for r in recs if r.node==1 and r.customer_class==1]
    >>> servicetimes_n2c1 = [r.service_time for r in recs if r.node==2 and r.customer_class==1]
    >>> arrivals_n1c0 = sorted([r.arrival_date for r in recs if r.node==1 and r.customer_class==0])
    >>> arrivals_n2c0 = sorted([r.arrival_date for r in recs if r.node==2 and r.customer_class==0])
    >>> arrivals_n1c1 = sorted([r.arrival_date for r in recs if r.node==1 and r.customer_class==1])
    >>> arrivals_n2c1 = sorted([r.arrival_date for r in recs if r.node==2 and r.customer_class==1])

Nawr gwelwn os yw'r amser gwasanaeth ac amser rhwng dyfodiad cymedrig yn cyfateb a'r dosraniadau::

    >>> from decimal import Decimal

    >>> sum(servicetimes_n1c0) / len(servicetimes_n1c0) # Disgwyl 0.1666...
    Decimal('0.1650563448')

    >>> sum(servicetimes_n2c0) / len(servicetimes_n2c0) # Disgwyl 0.4724...
    Decimal('0.4228601677')

    >>> sum(servicetimes_n1c1) / len(servicetimes_n1c1) # Disgwyl 0.4
    Decimal('0.4352210564')

    >>> sum(servicetimes_n2c1) / len(servicetimes_n2c1) # Disgwyl 0.4
    Decimal('0.4100529676')

    >>> set([r2-r1 for r1, r2 in zip(arrivals_n1c0, arrivals_n1c0[1:])]) # Dylai ond samplu 0.4
    {Decimal('0.4')}

    >>> set([r2-r1 for r1, r2 in zip(arrivals_n1c1, arrivals_n1c1[1:])]) # Dylai ond samplu 0.2
    {Decimal('0.2')}

    >>> expected_samples = {Decimal('0.2'), Decimal('0.1')} # Dylai ond samplu 0.1 a 0.2
    >>> set([r2-r1 for r1, r2 in zip(arrivals_n2c0, arrivals_n2c0[1:])]) == expected_samples
    True

    >>> expected_samples = {Decimal('0.2'), Decimal('0.4')}#  Dylai ond samplu 0.2 a 0.4
    >>> set([r2-r1 for r1, r2 in zip(arrivals_n2c1, arrivals_n2c1[1:])]) == expected_samples
    True

​