.. _until-numcusts:

=============================================
Sut i Efelychu Nes Nifer o Gwsmeriaid Penodol
=============================================

Gall terfynu rhediad efelychiad pan mae nifer penodol o gwsmeriaid wedi pasio trwyddo.
Gall wneud hwn gyda'r dull :code:`simulate_until_max_customers`.
Mae'r dull yn cymryd y ddadl :code:`max_customers`.
Mae yna tair ffordd o gyfri cwsmeriaid:

 - :code:`'Finish'`: Efelychu nes bod :code:`max_customers` wedi cyrraedd yr Exit Node.
 - :code:`'Arrive'`: Efelychu nes bod :code:`max_customers` wedi'i chreu yn yr Arrival Node.
 - :code:`'Accept'`: Efelychu nes bod :code:`max_customers` wedi'i chreu ac wedi'i derbyn (heb ei wrthod) yn yr Arrival Node.

Pennir y dull cyfri cwsmeriaid gyda'r ddadl opsiynol :code:`method`.
Y gwerth diofyn yw :code:`'Finish'`.

Ystyriwch system ciwio :ref:`M/M/1/3 <kendall-notation>`::

	>>> import ciw
	>>> N = ciw.create_network(
	...     Arrival_distributions=[['Exponential', 10]],
	...     Service_distributions=[['Exponential', 5]],
	...     Number_of_servers=[1],
	...     Queue_capacities=[3]
	... )

I efelychu nes bod 30 cwsmer wedi gorffen gwasanaeth::

	>>> ciw.seed(1)
	>>> Q = ciw.Simulation(N)
	>>> Q.simulate_until_max_customers(30, method='Finish')
	>>> len(Q.nodes[-1].all_individuals)
	30

I efelychu nes bod 30 cwsmer wedi cyrraedd::

	>>> ciw.seed(1)
	>>> Q = ciw.Simulation(N)
	>>> Q.simulate_until_max_customers(30, method='Arrive')
	>>> len(Q.nodes[-1].all_individuals), len(Q.nodes[1].all_individuals), len(Q.rejection_dict[1][0])
	(13, 3, 14)

I efelychu nes bod 30 cwsmer wedi'i derbyn::

	>>> ciw.seed(1)
	>>> Q = ciw.Simulation(N)
	>>> Q.simulate_until_max_customers(30, method='Accept')
	>>> len(Q.nodes[-1].all_individuals), len(Q.nodes[1].all_individuals)
	(26, 4)