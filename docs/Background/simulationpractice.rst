.. _simulation-practice:

=================
Arferion Efelychu
=================

Mae sicrhau arferion da wrth fodelu ac efelychu yn bwysig i gael modelau a dadansoddiadau ystyrlon.
Dangosir hwn yn :ref:`Tiwtorial IV <tutorial-iv>`.
Adnodd a argymhellir ar y pwnc yw [SW14]_.
Fe fydd y tudalen yma yn crynhoi rhai agweddau pwysig.

----------------------------
Perfformio Arbrofion Lluosog
----------------------------

Ni ddylai defnyddwyr dibynnu ar ganlyniadau rhediad sengl efelychiad oherwydd natur gynhenid stocastig efelychu.
Wrth redeg un arbrawf yn unig, ni all ddefnyddwyr gwybod os yw'r ymddygiad a ddangosir yn y rhediad yna yn nodweddiadol, eithafol neu'n anarferol.
I oresgyn hyn mae angen perfformio nifer o arbrofion, pob un yn defnyddio gwahanol lifoedd haprif.
Yna, gall perfformio dadansoddiadau ar ddosraniadau'r canlyniadau (er enghraifft  cymryd gwerthoedd cymedrig fel dangosyddion perfformiad allweddol).

Yn Ciw y ffordd symlaf o wneud hwn yw creu a rhedeg efelychiadau mewn lŵp, gan ddefnyddio hedyn gwahanol pob tro.

-------------
Amser Cynhesu
-------------

Yn aml nid yw modelau efelychiad yn dechrau mewn amgylchiadau realistig, hynny yw mai ganddynt gyflwr dechreuol afrealistig
Yn Ciw y cyflwr dechreuol yw system wag.
Wrth gwrs fe all fod sefyllfaoedd lle mae angen casglu canlyniadau o system wag, ond mewn sefyllfaoedd arall, er enghraifft wrth ddadansoddi systemau mewn cydbwysedd, mae'r cyflwr dechreuol yn achosi bias digroeso.
Un dull safonol o oresgyn hwn yw defnyddio amser cynhesu.
Rhedir yr efelychiad am gyfnod o amser (yr amser cynhesu) i sicrhau fod y system mewn cyflwr priodol cyn casglir canlyniadau.

Yn Ciw y ffordd symlaf o wneud hyn yw hidlo allan y canlyniadau a grëwyd yn ystod yr amser cynhesu.

----------
Amser Oeri
----------

Mae'r dull :code:`get_all_records` ond yn casglu cofnodion data gorffenedig.
Efallai bod angen casglu gwybodaeth dyfodi neu aros ar gwsmeriaid sydd dal yn ganol gwasanaeth.
Yn Ciw, gallwn wneud hyn trwy efelychu heibio diwedd y cyfnod arsylwi, ac yna ond casglu'r wybodaeth briodol o'r cyfnod arsylwi.

Yn Ciw y ffordd symlaf o wneud hyn yw hidlo allan y canlyniadau a grëwyd yn ystod yr amser oeri.



----------
Enghraifft
----------

Mae'r enghraifft isod yn dangos y ffordd symlaf o berfformio arbrofion lluosog, a defnyddio amser cynhesu ac amser oeri yn Ciw.
Mae'n dangos sut i ffeindio'r amser aros cymedrig mewn ciw :ref:`M/M/1 <kendall-notation>`::

    >>> import ciw
    >>> N = ciw.create_network(
    ...     arrival_distributions=[ciw.dists.Exponential(5.0)],
    ...     service_distributions=[ciw.dists.Exponential(8.0)],
    ...     routing=[[0.0]],
    ...     number_of_servers=[1]
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
    0.201313...

