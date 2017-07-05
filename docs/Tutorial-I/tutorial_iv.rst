.. _tutorial-iv:

=================================================
Tiwtorial IV: Arbrofion, Amser Twymo & Amser Oeri
=================================================

Yn Diwtorialau I-III fe ymchwilion ni un rhediad efelychiad o fanc.
Cyn gallwn ni dod i gasgliadau am ymddygiad y banc, mae yna gwpl o bethau rhaid i ni ystyried:

1. Fe wnaeth ein disgrifiad gwreiddiol o'r banc ei disgrifio fel bod ar agor 24/7. Mae hwn yn golygu bod y banc byth yn dechrau o gyflwr gwag, fel mae'r efelychiad yn.
2. Y cwsmeriaid sydd dal yn y system ar ddiwedd y rhediad: ni chasglwyd ei chofnodion data, er gwaethaf fod nhw wedi treulio amser yn y system yn ystod y cyfnod arsylwi.
3. A yw'r rhediad sengl yma yn adlewyrchu bywyd go iawn? A oedd y canlyniadau yma yn llyngyr? Yn arsylwad eithafol?

Fe all goresgyn y tri phryder yma gan ddefnyddio amser-twymo, amser-oeri, ac arbrofion, yn ôl ei eu trefn.
Mae disgrifiad llawn rhain ar gael :ref:`fan hyn <simulation-practice>`.

1. **Amser-twymo:** Efelychu'r system am ryw gyfnod amser cyn dechrau'r cyfnod arsylwi, felly nad yw'r system yn wag a bod y system mewn 'full swing' erbyn cychwyn y cyfnod arsylwi. Ond casglwch ganlyniadau o ddechrau'r cyfnod arsylwi.
2. **Amser-oeri:** Efelychu'r system am ryw gyfnod amser ar ôl diwedd y cyfnod arsylwi, felly nad oes unrhyw gwsmeriaid dan sylw yn sownd yn yr efelychiad pryd casglwyd canlyniadau. Ond casglwch ganlyniadau nes diwedd y cyfnod arsylwi.
3. **Arbrofion:** Efelychu'r system nifer o weithiau gyda llif rhifau ar hap gwahanol (gwahanol :ref:`hadau <set-seed>`). Cadwch holl ganlyniadau o dan ddiddordeb o'r holl arbrofion, felly gallwch gymryd cymedrau a chyfyngau hyder.

Gadwech i ni ddiffinio ein banc trwy greu gwrthrych Network::

    >>> import ciw
    >>> N = ciw.create_network(
    ...     Arrival_distributions=[['Exponential', 0.2]],
    ...     Service_distributions=[['Exponential', 0.1]],
    ...     Number_of_servers=[3]
    ... )

Am symlrwydd, fe fyddwn â diddordeb ffeindio'r amser aros cymedrig yn unig.
Rhedwn 10 efelychiad mewn lŵp, a chymryd amser-twymo ac amser-oeri o 100 uned amser.
Felly rhedwn bob arbrawf am 1 diwrnod + 200 munud (1640 munud)::

    >>> average_waits = []
    >>> for trial in range(10):
    ...     ciw.seed(trial)
    ...     Q = ciw.Simulation(N)
    ...     Q.simulate_until_max_time(1640)
    ...     recs = Q.get_all_records()
    ...     waits = [r.waiting_time for r in recs if r.arrival_date > 100 and r.arrival_date < 1540]
    ...     mean_wait = sum(waits) / len(waits)
    ...     average_waits.append(mean_wait)

Fe fydd y rhestr :code:`average_waits` yn cynnwys deg rhif, yr amser aros cymedrig o bob un o'r arbrofion.
Sylwch fe osodon ni hedyn gwahanol pob tro, fel bydd pob arbrawf yn rhoi canlyniadau gwahanol::

    >>> average_waits
    [3.23439..., 1.67172..., 3.81397..., 2.49197..., 4.53303..., 5.08311..., 3.64789..., 7.46596..., 7.12032..., 3.28304...]

Gwelwn fod ystod yr amseroedd aros yn uchel, rhwng 1.6 a 7.5.
Dangosir hyn ni fydd rhedeg un arbrawf yn unig yn rhoi ateb hyderus.
Fe allwn gymryd cymedr y canlyniadau dros yr arbrofion i gael ateb mwy hyderus::

    >>> sum(average_waits) / len(average_waits)
    4.23454...

Gan ddefnyddio Ciw, rydym wedi ffeindio fod cwsmeriaid yn aros 4.23 munud ar gyfartaledd mewn ciw yn y banc.
Beth fydd yn digwydd os ychwanegwn weinydd arall?
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

Trwy ychwanegu gweinydd arall fe allwn leihau'r amser aros cymedrig o 4.23 munud i 0.88 munud!
Da iawn, rydych chi wedi rhedeg eich senario beth-os cyntaf!
Mae senarios beth-os yn galluogi defnyddio efelychiad i weld os fydd newidiadau drud yn fuddiol i'r system, heb weithredu'r newidiadau drud hynny yn y system go iawn.
