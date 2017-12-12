.. _refs-statetrackers:

==============================================
Rhestr Tracwyr Cyflwr ar Gyfer Canfod Llwyrglo
==============================================

Ar hyn o bryd mae gan Ciw y tracwyr cyflwr canlynol:

- :ref:`naive`
- :ref:`matrix`


.. _naive:

--------------
Y Traciwr Naïf
--------------

Mae'r Traciwr Naïf yn recordio nifer of cwsmeriaid wrth bob nod, a faint o'r cwsmeriaid yna sydd wedi'i flocio'n bresennol.
Dangosir enghraifft o rwydwaith ciwio pedwar nod::

    ((3, 0), (1, 4), (10, 0), (8, 1))

Dynodir hwn 3 cwsmer wrth y nod cyntaf, mae 0 o rain wedi'i flocio; 5 cwsmer wrth yr ail nod, mae 4 o rain wedi'i flocio; 10 cwsmer wrth y trydydd nod, mae 0 o rain wedi'i flocio; a 9 cwsmer wrth y pedwerydd nod, mae 1 o rain wedi'i flocio.

Mae'r gwrthrych Simulation yn cymryd y ddadl opsiynol :code:`tracker`::

    >>> Q = ciw.Simulation(N, tracker='Naive') # doctest:+SKIP


.. _matrix:

-----------------
Y Traciwr Matrics
-----------------

Mae'r Traciwr Matrics yn cofnodi'r drefn a chyrchfannau'r cwsmeriaid a flociwyd mewn ffyrdd matrics.
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

    >>> Q = ciw.Simulation(N, tracker='Matrix') # doctest:+SKIP