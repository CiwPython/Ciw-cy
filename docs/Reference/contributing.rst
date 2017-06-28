.. _contributing:

--------------
Sut i Gyfrannu
--------------

========
Cyfrannu
========

Mae cyfraniadau o unrhywun yn anhygoel! Gall hyn cynnwyd agor `materion <https://github.com/CiwPython/Ciw/issues>`_, cyfarthrebu syniadau ar gyfer nodweddion newydd, gadael i ni wbod am defnydd y llyfrgell, a cyfraniadau cod. Carwn ni derbyn eich ceisiadau dynnu. Dyma canllawiau defnyddiol:

Fforciwch, yna clôniwch yr ystorfa::

    git clone git@github.com:your-username/Ciw.git

Gwnewch yn siŵr fod y profion yn pasio (defnyddir Ciw unittesting a doctesting)::

    python -m unittest discover ciw
    python doctests.py

Rydym yn anog defnydd coverage, yn iscrhau fod pob agwedd o'r cod wedi'i profi::

    coverage run --source=ciw -m unittest discover ciw.tests
    coverage report -m

Ychwanegwch profion ar gyfer eich newidiadau. Gwnewch eich newidiadau, a gwnewch yn siŵr fod y profion yn pasio.
Diweddarwch y dogfennaeth hefyd, yn sicrhau fod doctests yn pasio.

Gwthiwch eich fforc a chyflwynwch caid derbyn!

Rhai symiadau o le i dechrau:

- Edrychwch trwy ein `materion <https://github.com/CiwPython/Ciw/issues>`_.
- Agorwch materion newydd!
- Adroddiadau a trwsiadau byg.
- Tacluso cod a gwell perfformiad.
- Gwelliannau i'r `dogfennaeth <http://ciw.readthedocs.io>`_.
- Nodweddion newydd.

Edrychwn ymlaen i'ch cyfraniadau!