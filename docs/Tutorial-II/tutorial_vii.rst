.. _tutorial-vii:

========================================
Tiwtorial VII: Dosbarthau Cwsmer Lluosog
========================================

Dychmygwch glinig paediatregydd 24 awr:

+ Mae dau fath o glaf yn cyrraedd, babanod a phlant.
+ Pan gyrhaeddir cleifion mae angen iddynt gofrestru yn y dderbynfa.
+ Mae'r amser y mae'n cymryd i gofrestru ar hap, ond ar gyfer babanod mae'n para 15 munud ar gyfartaledd, ac ar gyfer plant mae'n para 10 munud ar gyfartaledd.
+ Ar ôl cofrestru mae'r ddau fath o glaf yn mynd i ystafelloedd aros gwahanol, lle maent yn aros ar gyfer arbenigwyr gwahanol.
+ Mae apwyntiad gydag arbenigwyr yn para am amser ar hap, ond yn para ar gyfartaledd un awr.
+ Mae yna un derbynnydd ar ddyletswydd, dau arbenigwr babanod, a tri arbenigwr plant ar ddyletswydd.
+ Mae babanod yn cyrraedd ar hap ar gyfradd un yr awr, a phlant ar gyfradd dau yr awr.

Yn y senario yma mae dau wahanol fath o gwsmer yn defnyddio'r un adnoddau, ond gallant nhw ddefnyddio'r adnoddau yma mewn gwahanol ffyrdd.
Mae Ciw yn delio gyda hwn trwy aseinio **dosbarthau cwsmer** i gwsmeriaid.
Yn y senario yma:

+ Aseinir babanod y dosbarth cwsmer :code:`'Class 0'`.
+ Aseinir plant y dosbarth cwsmer :code:`'Class 1'`.
+ Y dderbynfa yw Nod 1.
+ Yr arbenigwr babanod yw Nod 2.
+ Yr arbenigwr plant yw Nod 3.

Aseiniwn ymddygiad gwahanol i ddosbarthau cwsmer gwahanol trwy amnewid gwerthoedd allweddeiriau'r gwrthrych Network gyda geiriaduron, gyda dosbarthau cwsmer fel allweddau, a'r ymddygiad penodol fel gwerthoedd::

    >>> import ciw
    >>> N = ciw.create_network(
    ...     Arrival_distributions={'Class 0': [ciw.dists.Exponential(1.0)],
    ...                                        ciw.dists.NoArrivals(),
    ...                                        ciw.dists.NoArrivals()],
    ...                            'Class 1': [ciw.dists.Exponential(2.0),
    ...                                        ciw.dists.NoArrivals(),
    ...                                        ciw.dists.NoArrivals()]}
    ...     Service_distributions={'Class 0': [ciw.dists.Exponential(4.0)],
    ...                                        ciw.dists.Exponential(1.0)],
    ...                                        ciw.dists.Deterministic(0.0)],
    ...                            'Class 1': [ciw.dists.Exponential(6.0)],
    ...                                        ciw.dists.Deterministic(0.0)],
    ...                                        ciw.dists.Exponential(1.0)]]},
    ...     routing={'Class 0': [[0.0, 1.0, 0.0],
    ...                          [0.0, 0.0, 0.0],
    ...                          [0.0, 0.0, 0.0]],
    ...              'Class 1': [[0.0, 0.0, 1.0],
    ...                          [0.0, 0.0, 0.0],
    ...                          [0.0, 0.0, 0.0]]}, 
    ...     Number_of_servers=[1, 2, 3],
    ... )

Sylwch er rydym yn gwybod ni fydd dosbarthau cwsmer penodol angen gwasanaeth (er enghraifft ni fydd angen gweld arbenigwr plant ar fabanod: bydd cwsmeriaid Class 0 byth angen gwasanaeth yn Nod 3) mae dal angen mewnbynnu dosraniad gwasanaeth.
Dewiswn y dosraniad ffug :code:`ciw.dists.Deterministic(0.0)`.

Efelychwch y clinig am 9 awr::

    >>> Q = ciw.Simulation(N)
    >>> Q.simulate_until_max_time(9)
    >>> recs = Q.get_all_records()

Gwelwn nad oes unrhyw gwsmer Class 0 wedi cyrraedd Nod 3; ac nad oes unrhyw gwsmer Class 1 wedi cyrraedd Nod 2::

    >>> visited_by_babies = {1, 2}
    >>> set([r.node for r in recs if r.customer_class==0]) == visited_by_babies
    True

    >>> visited_by_children = {1, 3}
    >>> set([r.node for r in recs if r.customer_class==1]) == visited_by_children
    True

Hoffwn ffeindio'r amser aros cymedrig yn y dderbynfa, wrth yr arbenigwr babanod, ac wrth yr arbenigwr plant.
Efelychwn am 24 awr, yn defnyddio amser-twymo o 3 awr ac amser-oeri o 3 awr, ar 16 arbrawf.
Casglwn yr amseroedd aros cymedrig wrth bob nod am bob arbrawf::

	>>> average_waits_1 = []
	>>> average_waits_2 = []
	>>> average_waits_3 = []
	>>> for trial in range(16):
	...     ciw.seed(trial)
	...     Q = ciw.Simulation(N)
	...     Q.simulate_until_max_time(30)
	...     recs = Q.get_all_records()
	...     waits1 = [r.waiting_time for r in recs if r.node==1 and r.arrival_date > 3 and r.arrival_date < 27]
	...     waits2 = [r.waiting_time for r in recs if r.node==2 and r.arrival_date > 3 and r.arrival_date < 27]
	...     waits3 = [r.waiting_time for r in recs if r.node==3 and r.arrival_date > 3 and r.arrival_date < 27]
	...     average_waits_1.append(sum(waits1) / len(waits1))
	...     average_waits_2.append(sum(waits2) / len(waits2))
	...     average_waits_3.append(sum(waits3) / len(waits3))

Nawr ffeindiwn yr amser aros cymedrig dros yr arbrofion::

	>>> sum(average_waits_1) / len(average_waits_1)
    0.274301...

	>>> sum(average_waits_2) / len(average_waits_2)
    0.268752...

	>>> sum(average_waits_3) / len(average_waits_3)
    0.284763...

Mae'r canlyniadau yma yn dangos fod babanod yn aros 0.6 awr, tua 36 munud am apwyntiad.
Gall hwn cael ei ddefnyddio fel mesur gwaelodlin i gymharu unrhyw ailgyfluniadau potensial i'r clinig.