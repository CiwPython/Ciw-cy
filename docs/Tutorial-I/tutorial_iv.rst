.. _tutorial-iv:

=================================================
Tiwtorial IV: Arbrofion, Amser Twymo & Amser Oeri
=================================================

Yn Tiwtorialau I-III fe ymchwilion ni un rhediad efelychiad o banc.
Cyn allen ni dod i gasgliadau am ymddygiad y banc, mae yna cwpl o pethau rhaid i ni ystyried:

1. Fe wnaeth ein disgrifiad gwreiddiol o'r banc ei disgrifio fel bod ar agor 24/7. Mae hwn yn golygu bod y banc byth yn dechrau o cyflwr gwag, fel mae'r efelychiad yn.
2. Y cwsmeriaid sydd dal yn y system ar diwedd y rhediad: ni casglwyd ei cofnodion data, er gwaethaf fod nhw wedi gwario amser yn y system yn ystod y cyfnod arsylwi.
3. A yw'r rhediad sengl yma yn adlewyrchu bywyd go iawn? A oedd y canlyniadau yma yn lyngyr? Yn arsylwad eithafol?

Fe all goresgyn y tri pryder yma gan ddefnyddio amser-twymo, amser-oeri, ac arbrofion, yn ol ei eu trefn.
Mae disgrifiad llawn rhain ar gael :ref:`fan hyn <simulation-practice>`.

1. **Amser-twymo:** Efelychu'r system am rhyw cyfnod amser cyn dechrau y cyfnod arsylwi, felly nad yw'r system yn gwag a fod y system mewn 'full swing' erbyn cychwyn y cyfnod arsylwi. Ond casglwch canlyniadau o ddechrau'r cyfnod arsylwi.
2. **Amser-oeri:** Efelychu'r system am rhyw cyfnod amservar ol diwedd y cyfnod arsylwi, felly nad oes unrhyw cwsmeriaid dan sylw yn sownd yn yr efelychiad pryd casglwyd canlyniadau. Ond casglwych canlyniadau nes diwedd y cyfnod arsylwi.
3. **Arbrofion:** Efelychu'r system nifer o weithiau gyda llif rhifau ar hap gwahanol (gwahanol :ref:`hadau <set-seed>`). Cadwch holl canlyniadau o dan diddordeb o'r holl arbrofion, felly gallwch cymryd cymerdau a cyfyngau hyder.

Gadwech i ni diffinio ein banc trwy creu gwrthrych Network::

    >>> import ciw
    >>> N = ciw.create_network(
    ...     Arrival_distributions=[['Exponential', 0.2]],
    ...     Service_distributions=[['Exponential', 0.1]],
    ...     Number_of_servers=[3]
    ... )

Am simlrydd, fe fyddwn a diddordeb ffeindio'r amser aros cymedrig yn unig.
Rhedwn 10 efelychiad mewn lwp, a cymryd amser-twymo ac amser-oeri o 100 uned amser.
Felly rhedwn pob arbrawf am 1 diwrnod + 200 munud (1640 munud)::

    >>> average_waits = []
    >>> for trial in range(10):
    ...     ciw.seed(trial)
    ...     Q = ciw.Simulation(N)
    ...     Q.simulate_until_max_time(1640)
    ...     recs = Q.get_all_records()
    ...     waits = [r.waiting_time for r in recs if r.arrival_date > 100 and r.arrival_date < 1540]
    ...     mean_wait = sum(waits) / len(waits)
    ...     average_waits.append(mean_wait)

Fe fydd y list :code:`average_waits` yn cynnwys deg rhif, yr amser aros cymedrig o pob un o'r arbrofion.
Sylwch fe gododon ni hedyn gwahanol pob tro, fell bydd pob arbrawf yn rhoi canlyniadau gwahanol::

    >>> average_waits
    [3.23439..., 1.67172..., 3.81397..., 2.49197..., 4.53303..., 5.08311..., 3.64789..., 7.46596..., 7.12032..., 3.28304...]

Gwelwn fod ystod yr amseroedd aros yn uchel, rhwng 1.6 a 7.5.
Dangosir hyn ni fydd rhedeg un arbrawf yn unig yn rhoi ateb hyderus.
Fe allwn cymryd cymedr y canlyniadau dros yr arbrofion i cael ateb mwy hyderus::

    >>> sum(average_waits) / len(average_waits)
    4.23454...

Gan ddefnyddio Ciw, rydym wedi ffeindio fod cwsmeriaid yn aros 4.23 munud ar cyfartaledd mewn ciw yn y banc.
Beth fydd yn digwydd os ychwanegwn gweinydd arall?
Ail-adroddwch y dadansoddiad gyda 4 gweinydd::

    >>> N = ciw.create_network(
    ...     Arrival_distributions=[['Exponential', 0.2]],
    ...     Service_distributions=[['Exponential', 0.1]],
    ...     Number_of_servers=[4]
    ... )

    >>> average_waits = []
    >>> for trial in range(10):
    ...     ciw.seed(trial)
    ...     Q = ciw.Simulation(N)
    ...     Q.simulate_until_max_time(1640)
    ...     recs = Q.get_all_records()
    ...     waits = [r.waiting_time for r in recs if r.arrival_date > 100 and r.arrival_date < 1540]
    ...     mean_wait = sum(waits) / len(waits)
    ...     average_waits.append(mean_wait)

    >>> sum(average_waits) / len(average_waits)
    0.87878...

Trwy ychwanegu gweinydd arall fe allwn lleihau'r amser aros cymedrig o 4.23 munud i 0.88 munud!
Da iawn, rydych chi wedi rehedeg eich senario beth-os cyntaf!
Mae senarios beth-os yn galluogu defnyddio efelychiad i gweld os fydd newidiadau drud yn fuddiol i'r system, heb gweithredu'r newidiadau drud hwnna yn y system go iawn.
