.. _from-file:

====================================
Sut i Darllen ac Ygrifennu o/i Ffeil
====================================

Tra'n rhedeg arbrofion, fe all fod yn ddefnyddiol o darllen mewn paramedrau o ffeil, ac i all allforio cofnodion data i ffeil.
Gallwch wneud hwn yn hawdd gyda Ciw.
Fe all cynrychioli geiriaduron o paramedrau fel ffeiliau :code:`.yml`, a gall allforio canlyniadau fel ffeiliau :code:`.csv`.


Ffeiliau Paramedrau
~~~~~~~~~~~~~~~~~~~

Ystyriwch y rhwydwaith canlynol::

    >>> import ciw
	>>> N = ciw.create_network(
	...     Arrival_distributions={'Class 0': [['Exponential', 6.0], ['Exponential', 2.5]]},
	...     Service_distributions={'Class 0': [['Exponential', 8.5], ['Exponential', 5.5]]},
	...     Transition_matrices={'Class 0': [[0.0, 0.2], [0.1, 0.0]]},
	...     Number_of_servers=[1, 1],
	...     Queue_capacities=['Inf', 4]
	... )

Cynrychiolir hwn fel ffeil :code:`.yml` isod::

	parameters.yml

	Arrival_distributions:
	  Class 0:
	  - - Exponential
	    - 6.0
	  - - Exponential
	    - 2.5
	Service_distributions:
	  Class 0:
	  - - Exponential
	    - 8.5
	  - - Exponential
	    - 5.5
	Transition_matrices:
	  Class 0:
	  - - 0.0
	    - 0.2
	  - - 0.1
	    - 0.0
	Number_of_servers:
	- 1
	- 1
	Queue_capacities:
	- "Inf"
	- 4

Gallwch troi hwn mewn i gwrthrych Network yn defnyddio'r ffwythiant :code:`ciw.create_network_from_yml`::

	>>> import ciw # doctest:+SKIP
	>>> N = ciw.create_network_from_yml('<path_to_file>') # doctest:+SKIP
	>>> Q = ciw.Simulation(N) # doctest:+SKIP


Allforio Canlyniadau
~~~~~~~~~~~~~~~~~~~~

Unwaith bod efelychiad wedi'i rhedeg, gall ysgrifennu'r holl cofnodion data i ffeil gan ddefnyddio dull :code:`write_records_to_file` y gwrthrych Simulation.
Mae'r dull yma yn ysgrifenny'r holl canlyniadau a gafwyd gan y dull :code:`get_all_records` (gwelwch :ref:`fan hyn <refs-results>` am mwy o wybodaeth) i ffeil :code:`.csv`, lle mae pob rhes yw arsylwad a pob colofn yr newidyn::

	>>> Q.write_records_to_file('<path_to_file>') # doctest:+SKIP

Mae'r dull yma hefyd yn cymryd yr allweddair opsiynnol :code:`header`.
Os osodwyd hwn i :code:`True` yna bydd y rhes cyntaf yn cynnwys enwau'r newidynnau.
Yr opsiwn diofyn yw :code:`True`, gosodwch i :code:`False` os nad oes angen rhain::

	>>> Q.write_records_to_file('<path_to_file>', headers=True) # doctest:+SKIP
	>>> Q.write_records_to_file('<path_to_file>', headers=False) # doctest:+SKIP
