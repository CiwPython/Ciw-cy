.. _state-tracker:

==============
Tracwyr Cyflwr
==============

Mae gan Ciw'r opsiwn i actifeiddio traciwr cyflwr er mwyn tracio cyflwr y system wrth i'r efelychiad parhau. Yr opsiwn diofyn yw'r StateTracker sylfaenol sy'n gwneud dim (oni bai bod yr efelychiad yn canfod llwyrglo, felly NaiveTracker yw'r opsiwn diofyn). Mae gan y tracwyr cyflwr defnydd wrth efelychu nes llwyrglo, gan fod amseroedd i lwyrglo yn cael ei recordio ar gyfer pob cyflwr mae'r system yn cyrraedd.

Ar hyn o bryd mae gan Ciw'r tracwyr cyflwr canlynol:

- :ref:`naive`
- :ref:`matrix`


.. _naive:

--------------
Y Traciwr Naïf
--------------

Mae'r Traciwr Naïf yn recordio nifer o gwsmeriaid ym mhob nod, a faint o rain sydd wedi'i flocio. Mae enghraifft ar gyfer rhwydwaith pedwar nod wedi'i ddangos::

    ((3, 0), (1, 4), (10, 0), (8, 1))

Mae hwn yn dynodi 3 cwsmer yn y nod cyntaf, 0 o rain wedi blocio; 5 cwsmer yn yr ail nod, 4 o rain wedi blocio; 10 cwsmer yn y trydydd nod, 0 o rain wedi blocio; a 9 cwsmer yn y pedwerydd nod, 1 o rain wedi blocio.

Mae'r gwrthrych Simulation yn cymryd yr opsiwn :code:`Tracker` a ddefnyddwyd fel y ganlyn::

    >>> Q = ciw.Simulation(N, tracker='Naive') # doctest:+SKIP

.. _matrix:

-----------------
Y Traciwr Matrics
-----------------

Mae'r Traciwr Matrics yn recordio trefn a chyrchfan y blocio yn ffurf matrics. Yn ogystal â hwn mae nifer o gwsmeriaid ym mhob nod yn cael ei thracio. Mae'r gydran gyntaf, matrics, yn rhestru'r blocio o nod rhes i nod colofn. Rhestrau yw'r cofnodion, yn rhestru holl flocio o'r fath yma, ac mae'r rhifau tu fewn yn dynodi'r drefn caiff y cwsmeriaid yma ei flocio. Mae enghraifft wedi'i ddangos::

    ( ( ( (),  (),     (), ()  ),
        ( (),  (1, 4), (), (2) ),
        ( (),  (),     (), ()  ),
        ( (3), (),     (), ()  ) ),
      ( 3, 5, 10, 9) )

Mae hwn yn dynodi 3 cwsmer wrth y nod cyntaf, 5 cwsmer wrth yr ail nod, 10 cwsmer wrth y trydydd nod, a 9 cwsmer wrth y pedwerydd nod. Mae hefyd yn cynrychioli trefn y blocio. O'r cwsmeriaid sydd wedi'i flocio, y cyntaf i flocio oedd cwsmer yn nod 2 i nod 2; yr ail i flocio oedd y cwsmer yn nod 2 i nod 4; y trydydd i flocio oedd y cwsmer yn nod 4 i nod 1; a'r pedwerydd i flocio oedd y cwsmer yn nod 2 i nod 2.

Mae'r gwrthrych Simulation yn cymryd yr opsiwn :code:`Tracker` a ddefnyddwyd fel y ganlyn::

    >>> Q = ciw.Simulation(N, tracker='Matrix') # doctest:+SKIP
