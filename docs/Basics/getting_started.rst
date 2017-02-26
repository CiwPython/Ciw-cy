.. _getting-started:

==========
I Ddechrau
==========

Ystyriwch y rhwydwaith ciwio 2 nod canlynol:

.. image:: ../_static/2nodes.svg
   :scale: 100 %
   :alt: Rhwydwaith ciwio 2 nod.
   :align: center

Mae'r rhwydwaith ciwio yma yn cynnwys 2 nod:

* Nod 1 (Gwaelod)
	- Dyfodiadau Poisson ar gyfradd 6.0
	- Gwasanaethau esbonyddol ar gyfradd 8.5
	- Un gweinydd
	- Cynhwysedd ciwio anfeidrol
	- Tebygolrwydd 0.2 o ymuno â Nod 2 wedi gwasanaeth
* Nod 2 (Top)
	- Dyfodiadau Poisson ar gyfradd 2.5
	- Gwasanaethau esbonyddol ar gyfradd  5.5
	- Un gweinydd
	- Cynhwysedd ciwio macsimwm o 4
	- Tebygolrwydd 0.1 o ymuno â Nod 1 wedi gwasanaeth

Rydym yn dymuno efelychu'r system hon am 1000 uned amser. Mae'r system wedi'i ddiffinio gan y geiriadur paramedrau canlynol::

    >>> params = {
    ... 'Arrival_distributions': {'Class 0': [['Exponential', 6.0], ['Exponential', 2.5]]},
    ... 'Number_of_nodes': 2,
    ... 'Number_of_servers': [1, 1],
    ... 'Queue_capacities': ['Inf', 4],
    ... 'Number_of_classes': 1,
    ... 'Service_distributions': {'Class 0': [['Exponential', 8.5], ['Exponential', 5.5]]},
    ... 'Transition_matrices': {'Class 0': [[0.0, 0.2], [0.1, 0.0]]}
    ... }

Gwelwch :ref:`sim-parameters` am esboniad llawn o hwn.
Fe all Ciw defnyddio'r geiriadur paramedrau hwn i greu wrthrych Network, sy'n cael ei ddefnyddio i redeg yr efelychiad::

	>>> import ciw
	>>> N = ciw.create_network(params)
	>>> Q = ciw.Simulation(N)
	>>> Q.simulate_until_max_time(100)

Unwaith fod yr efelychiant wedi rhedeg, gall cael holl :ref:`results-data` trwy::

	>>> recs = Q.get_all_records()
