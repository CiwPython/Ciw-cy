.. _tutorial-vi:

======================================
Tiwtorial VI: Rhwydweithiau Cyfyngedig
======================================

Dychmygwch ffatri gweithgynhyrchu sy'n cynhyrchu stolion:

+ Pob 4 eiliad mae sedd yn cyrraedd ar gludfelt.
+ Mae'r cludfelt yn cynnwys tair gweithfan.
+ Wrth bob gweithfan mae coes yn cael ei chysylltu.
+ Mae cysylltu coes yn cymryd cyfnod o amser ar hap rhwng 3 eiliad a 5 eiliad.
+ Rhwng gweithfannau (a cyn y weithfan gyntaf) mae'r cludfan ond digon hir i dal 3 stôl.
+ Os yw'r cludfelt cyn y weithfan gyntaf yn llawn, mae stolion newydd yn cwympo i'r llawr ac yn torri.
+ Os yw'r stôl yn gorffen 'gwasanaeth' ar weithfan, ond nid oes lle ar y cludfelt, mae angen i'r stôl yna aros wrth y weithfan nes daeth lle ar y cludfan. Tra bod y blocio yma yn digwydd, ni all y weithfan yna cydosod unrhyw mwy o stolion. (Mae manylion llawn ar flocio ar gael :ref:`fan hyn <ciw-mechanisms>`.)

Mae pob stôl sy'n torri yn costio'r ffatri 10c mewn pren gwastraff.
Rydyn ni angen gwybod faint o stolion sy'n cwympo i'r llawr a thorri pob awr mae'r ffatri'n weithredol, ac felly'r gost gymedrig pob awr.
Yn gyntaf, diffiniwn ni'r Network.
Mae rhwydwaith cyfyngedig fel hwn wedi'i chynrychioli gan bron yr un gwrthrych Network a rhwydwaith anghyfyngedig, ond nawr ychwanegwn ni'r allweddair :code:`queue_capacities`::

    >>> import ciw
    >>> N = ciw.create_network(
    ...     1rrival_distributions=[ciw.dists.Deterministic(4.0),
    ...                            ciw.dists.NoArrivals(),
    ...                            ciw.dists.NoArrivals()],
    ...     service_distributions=[ciw.dists.Uniform(3, 5),
    ...                            ciw.dists.Uniform(3, 5),
    ...                            ciw.dists.Uniform(3, 5)],
    ...     routing=[[0.0, 1.0, 0.0],
    ...              [0.0, 0.0, 1.0],
    ...              [0.0, 0.0, 0.0]],
    ...     number_of_servers=[1, 1, 1],
    ...     queue_capacities=[3, 3, 3]
    ... )

Mae'r amser mae'n cymryd i atodi coes i stôl (yr amser gwasanaeth) wedi'i samplu o ddosraniad unffurf.
Mae'r dosraniad yma yn samplu pob gwerth rhwng terfyn isaf a therfyn uchaf.
Nodwch yr unedau amser fan hyn yw eiliadau.

Pan efelychwn ni hwn, gallwn weld gwybodaeth am y blocio, er enghraifft y cyfnod o amser gwariodd stôl wedi'i flocio ym mhob nod.
I weld hwn, gadewch i ni efelychu'r system am 20 munud::

    >>> ciw.seed(2)
    >>> Q = ciw.Simulation(N)
    >>> Q.simulate_until_max_time(1200)
    >>> recs = Q.get_all_records()

    >>> blockages = [r.time_blocked for r in recs]
    >>> max(blockages)
    1.402303...

Gwelwn fod yn 20 munud y cyfnod macsimwm gwariodd stôl wedi'i flocio yn weithfan oedd 1.5 eiliad.

Gallwn weld y wybodaeth ar y stolion a wnaeth cwympo bant o'r cludfelt gan ddefnyddio priodwedd :code:`rejection_dict` y gwrthrych Simulation.
Geiriadur yw hwn, sy'n mapio rhifau nod i eiriaduron.
Mae'r geiriaduron yma yn mapio rhifau dosbarthau cwsmer i restrau o ddyddiadau a chafodd cwsmeriaid eu gwrthod::

    >>> Q.rejection_dict
    {1: {0: [1020.0, 1184.0]}, 2: {0: []}, 3: {0: []}}

Yn y rhediad yma cafodd 3 stôl eu gwrthod (cwympo i'r llawr gan nad oedd lle ar y cludfelt) wrth Nod 1, ar ddyddiadau 740, 960, a 1140.
I gael nifer y stolion a chafodd eu gwrthod, cymerwch hyd y rhestr yma::

    >>> len(Q.rejection_dict[1][0])
    2

Rhedwn 8 arbrawf, a ffeindiwn nifer o wrthodion yr awr.
Cymerwn amser-twymo o 10 munud.
Ni fydd amser-oeri yn briodol gan ein bod ni'n recordio gwrthodion, sy'n digwydd ar y pwynt cyrraedd::

    >>> broken_stools = []
    >>> for trial in range(8):
    ...     ciw.seed(trial)
    ...     Q = ciw.Simulation(N)
    ...     Q.simulate_until_max_time(4200)
    ...     num_broken = len([r for r in Q.rejection_dict[1][0] if r > 600])
    ...     broken_stools.append(num_broken)

    >>> broken_stools
    [9, 10, 6, 9, 4, 7, 10, 3]

    >>> sum(broken_stools)/len(broken_stools)
    7.25

Ar gyfartaledd mae 7.25 stôl yn torri pob awr; yn costio 72.5c yr awr ar gyfartaledd.

Mae system cydosod newydd, yn costio £2500, yn gallu lleihau amrywiant yn amser atodi coes, fel bod hwn yn cymryd rhwng 3.5 a 4.5 eiliad i atodi coes.
Faint o oriau gweithredu sydd angen ar y ffatri i ennill nôl yr arian a wnaeth y system newydd gostio?

Yn gyntaf, o dan y system newydd faint o stolion rydym yn disgwyl torri pob awr?::

    >>> N = ciw.create_network(
    ...     arrival_distributions=[ciw.dists.Deterministic(4.0)],
    ...                            ciw.dists.NoArrivals(),
    ...                            ciw.dists.NoArrivals()],
    ...     service_distributions=[ciw.dists.Uniform(3.5, 4.5),
    ...                            ciw.dists.Uniform(3.5, 4.5),
    ...                            ciw.dists.Uniform(3.5, 4.5)],
    ...     routing=[[0.0, 1.0, 0.0],
    ...              [0.0, 0.0, 1.0],
    ...              [0.0, 0.0, 0.0]],
    ...     number_of_servers=[1, 1, 1],
    ...     queue_capacities=[3, 3, 3]
    ... )

    >>> broken_stools = []
    >>> for trial in range(8):
    ...     ciw.seed(trial)
    ...     Q = ciw.Simulation(N)
    ...     Q.simulate_until_max_time(4200)
    ...     num_broken = len([r for r in Q.rejection_dict[1][0] if r > 600])
    ...     broken_stools.append(num_broken)

    >>> sum(broken_stools) / len(broken_stools)
    0.875

Felly mae'r system newydd yn safio 6.375 stôl yr awr, tua 63.75c yr awr.
Felly fe fydd yn cymryd :math:`2500/0.6375 \approx 3921.57` awr gweithredu i'r system talu ar gyfer y system newydd.