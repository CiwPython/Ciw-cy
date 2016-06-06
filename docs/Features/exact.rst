.. _exact-simulations:

========
Manylder
========

Oherwydd y `problemau a cyfyngiadau <https://docs.python.org/2/tutorial/floatingpoint.html>`_ sy'n codi wrth delio â rhifau pwynt arnawf, mae Ciw yn cynnig opsiwn manylder. Byddwch yn ofalus, fodd bynnag, gall defnyddio'r opsiwn hon effeithio performiad, ac felly dylai ond ddefnyddio os yw problemau gyda rhifau pwynt arnawf yn effeithio'ch canlyniadau. Gall hwn digwydd wrth ddefnyddio dosraniadau penderfynedig ac amserlenni gwaith.

Er mwyn gweithredu manylder rhifyddeg, ychwanegwch yr opsiwn wrth greu'r wrthrych Simulation::

    >>> Q = ciw.Simulation(N, exact=26) # doctest:+SKIP

Mae'r opsiwn :code:`exact` yn dynodi'r lefel manyldeb.