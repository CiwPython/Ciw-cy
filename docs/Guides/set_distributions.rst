.. _set-dists:

==========================================
Sut i Osod Dosraniadau Dyfodi a Gwasanaeth
==========================================

Mae Ciw yn cynnig amrywiaeth o ddosraniadau amser rhwng-dyfodiad a gwasanaeth.
Ffeindiwch restr lawn :ref:`fan hyn <refs-dists>`.
Gwrthrychau ydynt, a ddiffinnir yn y gwrthrych Network gyda'r allweddeiriau :code:`'arrival_distributions'` a :code:`'service_distributions'`.

+ :code:`'Arrival_distributions'`: Dyma'r dosraniad a samplwyd amseroedd rhwng-dyfodiad. Hynny yw yr amser rhwng dau ddyfodiad olynol. Mae'n benodol ar gyfer nodau a dosbarthau cwsmer spesifig.
+ :code:`'Service_distributions'`: Dyma'r dosraniad a samplwyd amseroedd gwasanaeth. Hynny yw faint o amser mae cwsmer yn gwario gyda gweinydd (yn annibynnol o faint o weinyddion sydd yno). Mae'n benodol ar gyfer nodau a dosbarthau cwsmer spesifig.

Mae'r enghraifft ganlynol, gyda dau nod a dau ddosbarth cwsmer, y defnyddio wyth gwahanol ddosraniad dyfodi a gwasanaeth::

    >>> import ciw
    >>> N = ciw.create_network(
    ...     arrival_distributions={'Class 0': [ciw.dists.Deterministic(0.4),
    ...                                        ciw.dists.Empirical([0.1, 0.1, 0.1, 0.2])],
    ...                            'Class 1': [ciw.dists.Deterministic(0.2),
    ...                                        ciw.dists.Pmf([0.2, 0.4], [0.5, 0.5])]},
    ...     service_distributions={'Class 0': [ciw.dists.Exponential(6.0),
    ...                                        ciw.dists.Lognormal(-1, 0.5)],
    ...                            'Class 1': [ciw.dists.Uniform(0.1, 0.7),
    ...                                        ciw.dists.Triangular(0.2, 0.3, 0.7)]},
    ...     routing={'Class 0': [[0.0, 0.0], [0.0, 0.0]],
    ...              'Class 1': [[0.0, 0.0], [0.0, 0.0]]},
    ...     number_of_servers=[1, 1]
    ... )


Rhedwn hwn (gyda :ref:`rhifyddeg union <exact-arithmetic>`) am 25 uned amser::

    >>> ciw.seed(10)
    >>> Q = ciw.Simulation(N, exact=10)
    >>> Q.simulate_until_max_time(50)
    >>> recs = Q.get_all_records()

Mae'r system yn defnyddio'r wyth dosraniad canlynol:

+ :code:`ciw.dists.Deterministic(0.4)`:
   + Samplu 0.4 pob amser.
+ :code:`ciw.dists.Deterministic(0.2)`:
   + Samplu 0.2 pob amser.
+ :code:`ciw.dists.Empirical([0.1, 0.1, 0.1, 0.2])`:
   + Samplu'r rhifau 0.1, 0.1, 0.1 a 0.2 ar hap.
+ :code:`ciw.dists.Pmf([0.2, 0.4], [0.5, 0.5])`:
   + Samplu 0.2 hanner yr amser, a 0.4 hanner yr amser.
+ :code:`ciw.dists.Exponential(6.0)`:
   + Samplu o'r dosraniad `esbonyddol <https://en.wikipedia.org/wiki/Exponential_distribution>`_ gyda paramedr :math:`\lambda = 6.0`. Cymedr disgwyliedig o 0.1666...
+ :code:`ciw.dists.Uniform(0.1, 0.7)`:
   + Samplu unrhyw rhif rhwng 0.1 a 0.7 gyda tebygolrwydd hafal. Cymedr disgwyliedig o 0.4.
+ :code:`ciw.dists.Lognormal(-1, 0.5)`:
   + Samplu o;r dosraniad `lognormal <https://en.wikipedia.org/wiki/Log-normal_distribution>`_ gyda paramedrau :math:`\mu = -1` a :math:`\sigma = 0.5`. Cymedr disgwyliedig o 0.4724...
+ :code:`ciw.dists.Triangular(0.2, 0.3, 0.7)`:
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
    Decimal('0.1600313200')

    >>> sum(servicetimes_n2c0) / len(servicetimes_n2c0) # Disgwyl 0.4724...
    Decimal('0.4250531396')

    >>> sum(servicetimes_n1c1) / len(servicetimes_n1c1) # Disgwyl 0.4
    Decimal('0.4108660556')

    >>> sum(servicetimes_n2c1) / len(servicetimes_n2c1) # Disgwyl 0.4
    Decimal('0.3942034906')

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



Dosraniadau Gwstwm
------------------

Diffinir dosraniad trwy etifeddu o'r dosbarth cyffredinol :code:`ciw.dists.Distribution`.
Mae hwn yn galluogi defnyddwyr i diffinio'u dosraniadau ei hunain.

Ystyriwch dosraniad sy'n samplu'r gwerth `3.0` 50% o'r amser, ac yn samplu haprif unffurf rhwng 0 ac 1 fel arall. Gallwn ysgrifennu hwn trwy etifeddu o'r dosbarth cyffredinol, a diffinio dull :code:`sample` newydd::

    >>> import random
    >>> class CustomDistribution(ciw.dists.Distribution):
    ...     def sample(self, t=None, ind=None):
    ...         if random.random() < 0.5:
    ...             return 3.0
    ...         return random.random()

Gal rhoi hwn i mewn i'r gwrthrych :code:`Network` yn y ffordd arferol.


Dosraniadau Cyfunedig
---------------------

Gan fod gwrthrychau dosraniad yn edifeddu o'r dosbarth dosraniad cyffredinol, gall cael eu *cyfuno* trwy defnyddio'r gweithrediadau :code:`+`, :code:`-`, :code:`*`, ac :code:`/`.

Er enghraifft, gadewch i ni cyfuno dosraniad Esbonyddol a dosraniad Deterministig ym mhob un o'r pedwar ffordd::

    >>> Exp_add_Det = ciw.dists.Exponential(0.05) + ciw.dists.Deterministic(3.0)
    >>> Exp_sub_Det = ciw.dists.Exponential(0.05) - ciw.dists.Deterministic(3.0)
    >>> Exp_mul_Det = ciw.dists.Exponential(0.05) * ciw.dists.Deterministic(3.0)
    >>> Exp_div_Det = ciw.dists.Exponential(0.05) / ciw.dists.Deterministic(3.0)

Mae'r dosraniadau cyfunedig hyn yn rhoi'r cyfuniad o'r gwerthoedd a samplwyd:

    >>> ciw.seed(10)
    >>> [round(ciw.dists.Exponential(0.05).sample(), 2) for _ in range(5)]
    [16.94, 11.2, 17.26, 4.62, 33.57]
    >>> [round(ciw.dists.Deterministic(3.0).sample(), 2) for _ in range(5)]
    [3.0, 3.0, 3.0, 3.0, 3.0]

    >>> # Adio
    >>> ciw.seed(10)
    >>> [round(Exp_add_Det.sample(), 2) for _ in range(5)]
    [19.94, 14.2, 20.26, 7.62, 36.57]

    >>> # Tynnu
    >>> ciw.seed(10)
    >>> [round(Exp_sub_Det.sample(), 2) for _ in range(5)]
    [13.94, 8.2, 14.26, 1.62, 30.57]

    >>> # Lluosi
    >>> ciw.seed(10)
    >>> [round(Exp_mul_Det.sample(), 2) for _ in range(5)]
    [50.83, 33.61, 51.78, 13.85, 100.7]

    >>> # Rhannu
    >>> ciw.seed(10)
    >>> [round(Exp_div_Det.sample(), 2) for _ in range(5)]
    [5.65, 3.73, 5.75, 1.54, 11.19]

​