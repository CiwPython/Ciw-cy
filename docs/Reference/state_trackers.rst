.. _refs-statetrackers:

=====================
Rhestr Tracwyr Cyflwr
=====================

Ar hyn o bryd mae gan Ciw y tracwyr cyflwr canlynol:

- :ref:`population`
- :ref:`nodepop`
- :ref:`nodeclssmatrix`
- :ref:`naiveblock`
- :ref:`matrixblock`


.. _population:

--------------------------
Y Traciwr SystemPopulation
--------------------------

Mae'r traciwr SystemPopulation yn recordio'r nifer o gwsmeriaid yn y system cyfan, heb poeni pa nod y maent ynddo.
Mae cyflyrau ar ffurf rhif::

    4

Mae hwn yn dynodi bod pedwar cwsmer yn y system.

Mae'r gwrthrych Simulation yn cymryd y ddadl opsiynol :code:`tracker`::

    >>> Q = ciw.Simulation(N, tracker=ciw.trackers.SystemPopulation()) # doctest:+SKIP


.. _nodepop:

------------------------
Y Traciwr NodePopulation
------------------------

Mae'r traciwr NodePopulation yn recordio nifer o gwsmeriaid ym mhob nod.
Mae cyflyrau ar ffurf rhestr o rhifau. Mae enghraifft o rhwydwaith ciwio tri nod isod::

    (2, 0, 5)

Mae hwn yn dynodi bod dau cwsmer yn y nod cyntaf, dim cwsmer yn yr ail nod, a pump cwsmer yn y trydydd nod.

Mae'r gwrthrych Simulation yn cymryd y ddadl opsiynol :code:`tracker`::

    >>> Q = ciw.Simulation(N, tracker=ciw.trackers.NodePopulation()) # doctest:+SKIP


.. _nodeclssmatrix:

-------------------------
Y Traciwr NodeClassMatrix
-------------------------

Mae'r traciwr NodeClassPopulation yn recordio'r nifer o gwsmeriaid ym mhob nod, wedi'i sortio gan dosbarth cwsmer.
Mae cyflyrau ar ffurf matrics, hynny yw rhestr o restrau, lle mae bod rhes yn dynodi nod a pob colofn yn cynodi dosbarth cwsmer. Dangosir enghraifft o rhwydwaith ciwio tri nod gyda dau dosbarth cwsmer::

    ((3, 0),
     (0, 1),
     (4, 1))

Mae hwn yn dynodi bod:
  + Tri cwsmer yn y nod cyntaf - tri o Dosbarth 0, a dim o Dosbarth 1
  + Un cwsmer yn yr ail nod - dim i Dosbarth 0, ac un o Dosbarth 1
  + Pump cwsmer yn y trydydd nod - pedwar o Dosbarth 0, ac un o Dosbarth 1.

Mae'r gwrthrych Simulation yn cymryd y ddadl opsiynol :code:`tracker`::

    >>> Q = ciw.Simulation(N, tracker=ciw.trackers.NodeClassMatrix()) # doctest:+SKIP


.. _naiveblock:

-----------------------
Y Traciwr NaiveBlocking
-----------------------

Mae'r traciwr NaiveBlocking yn recordio nifer of cwsmeriaid wrth bob nod, a faint o'r cwsmeriaid yna sydd wedi'i flocio'n bresennol.
Dangosir enghraifft o rwydwaith ciwio pedwar nod::

    ((3, 0), (1, 4), (10, 0), (8, 1))

Dynodir hwn 3 cwsmer wrth y nod cyntaf, mae 0 o rain wedi'i flocio; 5 cwsmer wrth yr ail nod, mae 4 o rain wedi'i flocio; 10 cwsmer wrth y trydydd nod, mae 0 o rain wedi'i flocio; a 9 cwsmer wrth y pedwerydd nod, mae 1 o rain wedi'i flocio.

Mae'r gwrthrych Simulation yn cymryd y ddadl opsiynol :code:`tracker`::

    >>> Q = ciw.Simulation(N, tracker=ciw.trackers.NaiveBlocking()) # doctest:+SKIP


.. _matrixblock:

------------------------
Y Traciwr MatrixBlocking
------------------------

Mae'r traciwr MatrixBlocking yn cofnodi'r drefn a chyrchfannau'r cwsmeriaid a flociwyd mewn ffyrdd matrics.
Wrth ochr hwn cofnodir nifer o gwsmeriaid wrth bob nod.
Mae'r gydran gyntaf, matrics, yn rhestru'r cwsmeriaid a flociwyd o'r nod rhes i'r nod colofn.
Rhestrau o holl gwsmeriaid a flociwyd o'r math yma yw'r cofnodion, ac mae'r rhifau yn dynodi'r drefn a flociwyd y cwsmeriaid.
Dangosir esiampl o rwydwaith pedwar nod::

    ( ( ( (),  (),     (), ()  ),
        ( (),  (1, 4), (), (2) ),
        ( (),  (),     (), ()  ),
        ( (3), (),     (), ()  ) ),
      (3, 5, 10, 9) )

Mae hwn yn cynrychioli:

+ 3 cwsmer wrth y nod cyntaf
+ 5 cwsmer wrth yr ail nod
+ 10 cwsmer wrth y trydydd nod
+ 9 cwsmer wrth y pedwerydd nod

Mae hefyd yn dangos trefn a chyrchfannau’r cwsmeriaid a flociwyd:

+ Allan o'r holl gwsmeriaid a flociwyd, y cyntaf oedd o nod 2 i nod 2
+ Yr ail oedd o nod 2 i nod 4
+ Y trydydd oedd o nod 4 i nod 1
+ Y pedwerydd oedd o nod 2 i nod 2.

Mae'r gwrthrych Simulation yn cymryd y ddadl opsiynol :code:`tracker`::

    >>> Q = ciw.Simulation(N, tracker=ciw.trackers.MatrixBlocking()) # doctest:+SKIP
