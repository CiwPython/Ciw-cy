.. _simulation-practice:

=================
Arferion Efelychu
=================

Mae sicrhau arferion da wrth fodelu gydag efelychiadau yn bwysig er mwyn cael dadansoddiadau ystyrlon o'r modelau. Llyfr a argymhellir ar y pwnc yw 'Simulation: The practice of model development and use' gan Stewart Robinson. Mae'r tudalen yma yn crynhoi rhai agweddau pwysig o gynnal dadansoddiadau trwy efelychiad.

------------------------------
Perfformio Dyblygiadau Lluosog
------------------------------

Ni ddylai defnyddwyr dibynnu ar ganlyniadau rhediad sengl o'r efelychiad, oherwydd natur stocastig efelychiadau. Wrth redeg un dyblygiad yn unig, ni allai defnyddwyr gwybod os yw'r ymddygiad a welir yn nodweddiadol, eithafol neu'n anarferol. I ddod dros hwn mae angen perfformio dyblygiadau lluosog, yn defnyddio ffrwd haprif gwahanol pob tro. Yna, fe allwch ddadansoddi canlyniadau'r dosraniadau canlyniadau (er enghraifft gan gymryd gwerthoedd cymedrig y dangosyddion perfformiad allweddol.)

Yn Ciw, y ffordd symlaf o weithredu hwn yw creu a rhedeg yr efelychiad mewn lŵp, gan osod hedyn ffrwd haprif gwahanol pob tro.

-------------
Amser Cynhesu
-------------

Fel arfer mae efelychiadau yn dechrau o dan amgylchiadau afrealistig, hynny yw mai ganddyn nhw amodau cychwynnol afrealistig. Yn Ciw, yr amodau cychwynnol diofyn yw system wag. Wrth gwrs fe all fod yna sefyllfaoedd lle mae angen casglu'r holl ganlyniadau o system wag, ond mewn sefyllfaoedd arall, er enghraifft wrth ddadansoddi systemau mewn cydbwysedd, mae'r amodau cychwynnol yn achosi bias digroeso. Un dull safonol o oroesi hwn yw defnyddio amser cynhesu. Rhed yr efelychiad amser penodol (yr amser cynhesu) i gael y system mewn cyflwr priodol cyn bod unrhyw ganlyniadau yn cael ei gasglu.

Yn Ciw, y ffordd symlaf o weithredu hwn yw hidlo mas unrhyw record a chrëwyd cyn yr amser cynhesu.

Mae'r enghraifft isod yn dangos y ffordd symlaf o berfformio dyblygiadau lluosog, a defnyddio amser cynhesu, yn Ciw. Mae'n dangos sut i ffeindio'r amser aros cymedrig ar gyfer ciw M/M/1::

    >>> import ciw
    >>> params = {'Arrival_distributions': [['Exponential', 5.0]],
    ...           'Service_distributions': [['Exponential', 8.0]],
    ...           'Transition_matrices': [[0.0]],
    ...           'Number_of_servers': [1]}
    >>>
    >>> average_waits = []
    >>> warmup = 50
    >>>
    >>> for s in range(100):
    ...     ciw.seed(s)
    ...     N = ciw.create_network(params)
    ...     Q = ciw.Simulation(N)
    ...     Q.simulate_until_max_time(200)
    ...     recs = Q.get_all_records()
    ...     waits = [r.waiting_time for r in recs if r.arrival_date > warmup]
    ...     average_waits.append(sum(waits)/len(waits))
    >>>
    >>> average_wait = sum(average_waits)/len(average_waits)
    >>> print(round(average_wait, 5))
    0.21071

