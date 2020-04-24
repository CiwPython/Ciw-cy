.. _tutorial-v:

================================
Tiwtorial V: Rhwydwaith o Giwiau
================================

Mae pŵer go iawn Ciw yn dod wrth fodelu rhwydwaith o giwiau.
Hynny yw nifer o nodau gwasanaeth, fel bod pan mae cwsmer yn gorffen gwasanaeth, mae yna debygolrwydd o ymuno a nod arall, ail-ymuno a'r nod presennol, neu adael y system.

Dychmygwch gaffi sy'n gwerthu bwyd poeth ac oer.
Gall cwsmeriaid cymryd nifer o lwybrau:

+ Mae angen i gwsmeriaid sydd ond eisiau bwyd oer ciwio wrth y cownter bwyd oer, ac yna cymryd eu bwyd i'r til i dalu.
+ Mae angen i gwsmeriaid sydd ond eisiau bwyd poeth ciwio wrth y cownter bwyd poeth, ac yna cymryd eu bwyd i'r til i dalu.
+ Mae angen i gwsmeriaid sydd eisiau bwyd oer a bwyd poeth ciwio yn gyntaf ar gyfer bwyd oer, yna ar gyfer bwyd poeth, ac yna cymryd y ddau i'r til i dalu.

Yn y system yma mae yna tri nod: Cownter bwyd oer (Nod 1), Cownter bwyd poeth (Nod 2), a'r til (Nod 3):

+ Mae cwsmeriaid sydd ond eisiau bwyd poeth yn cyrraedd ar gyfradd 12 yr awr.
+ Mae cwsmeriaid sydd eisiau bwyd oer yn cyrraedd ar gyfradd 18 yr awr.
+ Mae 30% o'r holl gwsmeriaid sydd eisiau prynu bwyd oer hefyd eisiau prynu bwyd poeth.
+ Ar gyfartaledd mae'n cymryd 1 munud i weini bwyd oer, 2 a hanner munud i weini bwyd poeth, a 2 munud i dalu.
+ Mae yna 1 gweinydd wrth y cownter bwyd oer, 2 weinydd wrth y cownter bwyd poeth, a 2 weinydd wrth y til.

Dangosir diagram o'r system isod:

.. image:: ../_static/cafe.svg
   :alt: Diagram o'r rhwydwaith ciwio caffi.
   :align: center

Gellir disgrifio'r system yma mewn un gwrthrych Network.
Rhestrir y dosraniadau dyfodi a gwasanaeth a nifer y gweinyddion yn drefn y nodau.
Mae hefyd angen *matrics trosglwyddo*.

Matrics trosglwyddo yw matrics :math:`n \times n` (lle :math:`n` yw nifer y nodau yn y rhwydwaith) fel bod yr elfen :math:`(i,j)\text{fed}` yn cyfateb i'r tebygolrwydd o drosglwyddo i nod :math:`j` ar ôl gorffen gwasanaeth yn nod :math:`i`.
Mae matrics trosglwyddo'r caffi yn edrych fel hyn:

.. math::

    \begin{pmatrix}
    0.0 & 0.3 & 0.7 \\
    0.0 & 0.0 & 1.0 \\
    0.0 & 0.0 & 0.0 \\
    \end{pmatrix}


Hynny yw mai 30% o'r cwsmeriaid bwyd oer yn mynd ymlaen i'r cownter bwyd poeth, tra bod y 70% sy'n weddill yn mynd i'r til, ac mae 100% o gwsmeriaid bwyd poeth yn mynd ymlaen i'r til.
Felly mae Network y caffi yn edrych fel hyn::

    >>> import ciw
    >>> N = ciw.create_network(
    ...     arrival_distributions=[ciw.dists.Exponential(0.3),
    ...                            ciw.dists.Exponential(0.2),
    ...                            ciw.dists.NoArrivals()],
    ...     service_distributions=[ciw.dists.Exponential(1.0),
    ...                            ciw.dists.Exponential(0.4),
    ...                            ciw.dists.Exponential(0.5)],
    ...     routing=[[0.0, 0.3, 0.7],
    ...              [0.0, 0.0, 1.0],
    ...              [0.0, 0.0, 0.0]],
    ...     number_of_servers=[1, 2, 2]
    ... )

Sylwch y dosraniadau dyfodi:
mae 18 dyfodiad bwyd oer yn gyfatebol i :code:`0.3` y munud; mae 12 dyfodiad bwyd poeth yn gyfatebol i :code:`0.2` y munud; ac nid oes unrhyw ddyfodiadau wrth y til.

Sylwch y dosraniadau gwasanaeth:
mae amser gwasanaeth bwyd oer cymedrig o 1 munud yn gyfatebol i gyfradd o 1/1 = :code:`1` gwasanaeth y munud; mae amser gwasanaeth bwyd poeth cymedrig o 2.5 munud yn gyfatebol i 1/2.5 = :code:`0.4` gwasanaeth y munud; ac mae amser gwasanaeth cymedrig o 2 munud wrth y til yn gyfatebol i :code:`0.5` gwasanaeth y munud.

Gadewch i ni efelychu'r system yma am un sifft amser cinio o 3 awr (180 munud).
Ar ddechrau amser cinio mae'r caffi yn agor, felly mae'r system yn dechrau yn wag.
Felly nad oes angen amser-cynhesu.
Defnyddiwn 20 munud o amser-oeri.
Rhedwn 10 arbrawf, i gael mesur nifer cymedrig cwsmeriaid sy'n pasio trwy'r system.
I ffeindio'r nifer cymedrig o gwsmeriaid sy'n pasio trwy'r system, gallwn gyfri'r nifer o gofnodion data sydd wedi pasio trwy Nod 3 (y til)::

    >>> completed_custs = []
    >>> for trial in range(10):
    ...     ciw.seed(trial)
    ...     Q = ciw.Simulation(N)
    ...     Q.simulate_until_max_time(200)
    ...     recs = Q.get_all_records()
    ...     num_completed = len([r for r in recs if r.node==3 and r.arrival_date < 180])
    ...     completed_custs.append(num_completed)

Nawr gallwn gael nifer cymedrig o gwsmeriaid sydd wedi pasio trwy'r system::

    >>> sum(completed_custs) / len(completed_custs)
    81.9

Felly rydym wedi defnyddio Ciw i ffeindio fod y caffi medru weini nifer cyfartaledd o 81.9 cwsmer mewn sifft amser cinio o dair awr.