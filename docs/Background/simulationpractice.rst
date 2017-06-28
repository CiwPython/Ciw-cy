.. _simulation-practice:

=================
Arferion Efelychu
=================

Mae sicrhau arferion da with modelu ac efelychu yn bwysig i cael modelau a dadansoddiadau ystyrlon.
Dangosir hwn yn :ref:`Tiwtorial IV <tutorial-iv>`.
Adnodd a argymhellir ar y pwnc yw [SW14]_.
Fe fydd y tudalen yma yn crynhoi rhai agweddau pwysig.

----------------------------
Perfformio Arbrofion Lluosog
----------------------------

Ni ddylai defnyddwyr dibynnu ar canlyniadau rhediad sengl efelychiad oherwydd natur cynhenid stocastig efelychu.
Pan yn rhedeg un arbrawf yn unig, ni all ddefnyddwyr gwybod os yw'r ymddygiad a ddangosir yn y rhediad yna yn nodweddiadol, eithafol neu'n anarferol.
I goresgyn hyn mae angen perfformio nifer o arbrofio, pob un yn defnyddio gwahanol llifau haprhif.
Yna, gall perfformio dadansoddiadau ar dosraniadau y canlyniadau (er enghraifft  cymryd gwerthoedd cymedrig fel dangosyddion perfformiad allweddol).

Yn Ciw y ffordd simplad o wneud hwn yw i creu a rhedeg efelychiadau mewn lŵp, gan ddefnyddio hedyn gwahanol pob tro.

-------------
Amser Cynhesu
-------------

Yn amal nid yw modelau efelychiad yn dechrau mewn amgylchiadau realistig, hynny yw mae ganddynt cyflwr dechreuol afrealistig
Yn Ciw y cyflwr dechreuol yw system gwag.
Wrth gwrs fe all fod sefyllfaoedd lle mae angen casglu canlyniadau o system gwag, ond mewn sefyllfaoedd arall, er enghraifft pan yn dadansoddi systemau mewn cydbwysedd, mae'r cyflwr dechreuol yn achosu bias digroeso.
Un dull safonol o goresgyn hwn yw i ddefnyddio amser cynhesu.
Rhedir yr efelychiad am cyfnod o amser (yr amser cynhesu) i sicrhau fod y system mewn cyflwr priodol cyn casglir canlyniadau.

Yn Ciw y ffordd simlaf o wneud hyn yw i hildo allan y canlyniadau a grëwyd yn ystod yr amser cynhesu.

----------
Amser Oeri
----------

Mae'r method :code:`get_all_records` ond yn casglu cofnodion data gorffenedig.
Efallai bod angen casglu gwybodaeth dyfodi neu aros ar cwsmeriaid sydd dal yn canol gwasnaeth.
Yn Ciw, gallwn gwneud hyn trwy efelychu heibio diwedd y cyfnod arsylwi, ac yna ond casglu'r gwybodaeth priodol o'r cyfnod arsylwi.

Yn Ciw y ffordd simlaf o wneud hyn yw i hidlo allan y canlyniadau a grëwyd yn ystod yr amser oeri.



----------
Enghraifft
----------

Mae'r enghraifft isod yn dangos y ffordd simlaf o perfformio arbrofion lluosog, a ddefnyddio amser cynhesu ac amser oeri yn Ciw.
Mae'n dangos sut i ffeindio'r amser aros cymedrig mewn ciw :ref:`M/M/1 <kendall-notation>`::

    >>> import ciw
    >>> N = ciw.create_network(
    ...     Arrival_distributions=[['Exponential', 5.0]],
    ...     Service_distributions=[['Exponential', 8.0]],
    ...     Transition_matrices=[[0.0]],
    ...     Number_of_servers=[1]
    ... )
    >>>
    >>> average_waits = []
    >>> warmup = 10
    >>> cooldown = 10
    >>> maxsimtime = 40
    >>>
    >>> for s in range(25):
    ...     ciw.seed(s)
    ...     Q = ciw.Simulation(N)
    ...     Q.simulate_until_max_time(warmup + maxsimtime + cooldown)
    ...     recs = Q.get_all_records()
    ...     waits = [r.waiting_time for r in recs if r.arrival_date > warmup and r.arrival_date < warmup + maxsimtime]
    ...     average_waits.append(sum(waits) / len(waits))
    >>>
    >>> average_wait = sum(average_waits) / len(average_waits)
    >>> average_wait
    0.204764...

