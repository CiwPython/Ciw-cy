.. _contributing:

--------------
Sut i Gyfrannu
--------------

========
Cyfrannu
========

Mae cyfraniadau o unrhyw un yn anhygoel! Gall hyn cynnwyd agor `materion <https://github.com/CiwPython/Ciw/issues>`_, cyfarthrebu syniadau ar gyfer nodweddion newydd, gadael i ni wbod am defnydd y llyfrgell, a cyfraniadau cod. Carwn ni derbyn eich ceisiadau dynnu. Dyma ganllawiau defnyddiol:

Fforciwch, yna clôniwch yr ystorfa::

    git clone git@github.com:your-username/Ciw.git

Gwnewch yn siŵr fod y profion yn pasio (defnyddir Ciw unittesting a doctesting)::

    python -m unittest discover ciw
    python doctests.py

Rydym yn annog defnydd coverage, yn sicrhau fod pob agwedd o'r cod wedi'i phrofi::

    coverage run --source=ciw -m unittest discover ciw.tests
    coverage report -m

Ychwanegwch brofion ar gyfer eich newidiadau. Gwnewch eich newidiadau, a gwnewch yn siŵr fod y profion yn pasio.

Diweddarwch y ddogfennaeth hefyd, yn sicrhau fod doctests yn pasio.
Er mwyn adeiladu'r dogfennaeth (mae angen `Sphinx <https://www.sphinx-doc.org/en/master/>`_)::
    
    cd docs
    make html

Gwthiwch eich fforc a chyflwynwch gais derbyn!

Rhai syniadau o le i ddechrau:

- Edrychwch trwy ein `materion <https://github.com/CiwPython/Ciw/issues>`_.
- Agorwch faterion newydd!
- Adroddiadau a trwsiadau byg.
- Tacluso cod a gwell perfformiad.
- Gwelliannau i'r `dogfennaeth <http://ciw.readthedocs.io>`_.
- Nodweddion newydd.

Edrychwn ymlaen at eich cyfraniadau!