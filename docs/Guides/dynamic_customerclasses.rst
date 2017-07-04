.. _dynamic-classes:

=====================================
Sut i Osod Dosbarthau Cwsmer Deinamig
=====================================

Mae Ciw yn gadael i cwsmeriaid newid eu dosbarth cwsmer yn tebygoliaethol ar ôl gorffen gwasanaeth.
Hynny yw ar ôl gwasanaeth yn od `k` mae cwsmer dosbarth `i` yn newid i fod yn dosbarth `j` gyda tebygolrwydd :math:`P(J=j \; | \; I=i, K=k)`.
Mewnbynnir y tebygolrwyddau yma trwy'r allweddair :code:`Class_change_matrices`.

Ystyriwch system un nod gyda tri dosbarth cwsmer.
Ar ôl wasanaeth (yn Nod 1) mae cwsmeriaid pendant yn newid dosbarth cwsmer, yr un mor debygol rhwng y dau dosbarth cwsmer arall.
Dangosir y :code:`Class_change_matrices` ar gyfer y system yma:

.. math::

    \begin{pmatrix}
    0.0 & 0.5 & 0.5 \\
    0.5 & 0.0 & 0.5 \\
    0.5 & 0.5 & 0.0 \\
    \end{pmatrix}


Mewnbynnir hwn i mewn i'r model efelychu trwy ychwanegu'r allweddair :code:`Class_change_matrices` tra'n creu gwrthrych Network::
    
    >>> import ciw
    >>> N = ciw.create_network(
    ...     Arrival_distributions={'Class 0': [['Exponential', 5]],
    ...                            'Class 1': ['NoArrivals'],
    ...                            'Class 2': ['NoArrivals']},
    ...     Service_distributions={'Class 0': [['Exponential', 10]],
    ...                            'Class 1': [['Exponential', 10]],
    ...                            'Class 2': [['Exponential', 10]]},
    ...     Transition_matrices={'Class 0': [[1.0]],
    ...                          'Class 1': [[1.0]],
    ...                          'Class 2': [[1.0]]},
    ...     Class_change_matrices={'Node 1': [[0.0, 0.5, 0.5],
    ...                                       [0.5, 0.0, 0.5],
    ...                                       [0.5, 0.5, 0.0]]},
    ...     Number_of_servers=[1]
    ... )

Nodwch yn y rhwydwaith yma ond dyfodiadau o dosbarth cwsmeriaid 0 a ddigwyddir.
Yn rhedeg y system yma, gwelwn fod nifer cofnodion gan cwsmeriaid o ddosbarth 1 a 2 yn fwy na sero, gan fod rhai cwsmeriaid dosbarth 0 wedi newid dosbarth cwsmer ar ôl gwasanaeth::

    >>> from collections import Counter
    >>> ciw.seed(1)
    >>> Q = ciw.Simulation(N)
    >>> Q.simulate_until_max_time(50.0)
    >>> recs = Q.get_all_records()
    >>> Counter([r.customer_class for r in recs])
    Counter({0: 255, 2: 125, 1: 105})

Nodwch pan ddefnyddir mwy nag un nod, mae angen matrics newid dosbarth ar pob nod.
Mae hwn yn golygu gall matrics gwahanol cael ei ddefnyddio ar gyfer pob nod.