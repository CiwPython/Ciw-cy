.. _from-file:

======================================
Sut i Ddarllen ac Ysgrifennu o/i Ffeil
======================================

Wrth redeg arbrofion, fe all fod yn ddefnyddiol o ddarllen mewn paramedrau o ffeil, ac i all allforio cofnodion data i ffeil.
Gallwch wneud hwn yn hawdd gyda Ciw.
Fe all cynrychioli geiriaduron o baramedrau fel ffeiliau :code:`.yml`, a gall allforio canlyniadau fel ffeiliau :code:`.csv`.


Ffeiliau Paramedrau
~~~~~~~~~~~~~~~~~~~

Ystyriwch y rhwydwaith canlynol::

    >>> import ciw
	>>> N = ciw.create_network(
	...     arrival_distributions={'Class 0': [ciw.dists.Exponential(6.0), ciw.dists.Exponential(2.5)]},
	...     service_distributions={'Class 0': [ciw.dists.Exponential(8.5), ciw.dists.Exponential(5.5)]},
	...     routing={'Class 0': [[0.0, 0.2], [0.1, 0.0]]},
	...     number_of_servers=[1, 1],
	...     queue_capacities=[float('inf'), 4]
	... )

Cynrychiolir hwn fel ffeil :code:`.yml` isod::

	parameters.yml

	arrival_distributions:
	  Class 0:
	  - - Exponential
	    - 6.0
	  - - Exponential
	    - 2.5
	service_distributions:
	  Class 0:
	  - - Exponential
	    - 8.5
	  - - Exponential
	    - 5.5
	routing:
	  Class 0:
	  - - 0.0
	    - 0.2
	  - - 0.1
	    - 0.0
	number_of_servers:
	- 1
	- 1
	queue_capacities:
	- "Inf"
	- 4

Gallwch droi hwn mewn i wrthrych Network yn defnyddio'r ffwythiant :code:`ciw.create_network_from_yml`::

	>>> import ciw # doctest:+SKIP
	>>> N = ciw.create_network_from_yml('<path_to_file>') # doctest:+SKIP
	>>> Q = ciw.Simulation(N) # doctest:+SKIP


Allforio Canlyniadau
~~~~~~~~~~~~~~~~~~~~

Unwaith bod efelychiad wedi'i rhedeg, gall ysgrifennu'r holl gofnodion data i ffeil gan ddefnyddio dull :code:`write_records_to_file` y gwrthrych Simulation.
Mae'r dull yma yn ysgrifennu'r holl ganlyniadau a gafwyd gan y dull :code:`get_all_records` (gwelwch :ref:`fan hyn <refs-results>` am fwy o wybodaeth) i ffeil :code:`.csv`, lle mae pob rhes yw arsylwad a pob colofn y newidyn::

	>>> Q.write_records_to_file('<path_to_file>') # doctest:+SKIP

Mae'r dull yma hefyd yn cymryd yr allweddair opsiynol :code:`header`.
Os osodwyd hwn i :code:`True` yna bydd y rhes gyntaf yn cynnwys enwau'r newidynnau.
Yr opsiwn diofyn yw :code:`True`, gosodwch i :code:`False` os nad oes angen y rhain::

	>>> Q.write_records_to_file('<path_to_file>', headers=True) # doctest:+SKIP
	>>> Q.write_records_to_file('<path_to_file>', headers=False) # doctest:+SKIP
