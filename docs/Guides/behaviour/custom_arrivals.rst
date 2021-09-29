Dyfodiadau Cyflwr-dibynnol
==========================

Yn yr enghraifft hon byddwn yn ystyried rhwydwaith o gwsmeriaid sy'n cyrraedd i wahanol nodau yn dibynnu ar cyflwr y system. Edrychwn ar system heb yr ymddygiad hwn yn gyntaf, ac yna'r system gyda'r ymddygiad dymunol, i'w gymharu.


Heb yr ymddygiad dymunol
~~~~~~~~~~~~~~~~~~~~~~~~

Ystyriwch y rhwydwaith dau nod canlynol, lle mae dyfodiadau ond yn digwydd yn y nod cyntaf, ac mae cynhwysedd ciwio o 10. Mae'r ail nod yn segur ac yn ddiangen yn y senario hon::

	>>> import ciw
	>>> from collections import Counter

	>>> N = ciw.create_network(
	...     arrival_distributions=[ciw.dists.Exponential(6.0), ciw.dists.NoArrivals()],
	...     service_distributions=[ciw.dists.Exponential(5.0), ciw.dists.Exponential(5.0)],
	...     routing=[[0.0, 0.0], [0.0, 0.0]],
	...     number_of_servers=[1, 1],
	...     queue_capacities=[10, float('inf')]
	... )

Nawr rhedwn y system am 100 uned amser, a gwelwn cawn 494 gwasanaeth yn y nod cyntaf, a dim yn yr ail nod::

	>>> ciw.seed(1)
	>>> Q = ciw.Simulation(N)
	>>> Q.simulate_until_max_time(100)

	>>> service_nodes = [r.node for r in Q.get_all_records()]
	>>> Counter(service_nodes)
	Counter({1: 494})



Gyda'r ymddygiad dymunol
~~~~~~~~~~~~~~~~~~~~~~~~

Nawr byddwn yn creu :code:`CustomArrivalNode` newydd fel bod cwsmeriaid sy'n cyrraedd pan mae gan y nod cyntaf 10 neu mwy o gwsmeriaid yn bresenol yn cael eu hanfon i'r ail nod.
Yn gyntaf mae'r :code:`CustomArrivalNode` yn etifeddu o :code:`ciw.ArrivalNode`, ac yn trosysgrifo'r dull :code:`send_individual`::

	>>> class CustomArrivalNode(ciw.ArrivalNode):
	...     def send_individual(self, next_node, next_individual):
	...         """
	...         Yn anfon y next_individual i'r next_node
	...         """
	...         self.number_accepted_individuals += 1
	...         if len(next_node.all_individuals) <= 10:
	...             next_node.accept(next_individual)
	...         else:
	...             self.simulation.nodes[2].accept(next_individual)

Er mwyn rhedeg y system, mae angen cael gwared a'r arg :code:`queue_capacities` wrth creu'r rhwydwaith, fel nad yw cwsmeriaid yn cael ei gwrthod cyn cyrraedd y dull :code:`send_individual` method::

	>>> N = ciw.create_network(
	...     arrival_distributions=[ciw.dists.Exponential(6.0), ciw.dists.NoArrivals()],
	...     service_distributions=[ciw.dists.Exponential(5.0), ciw.dists.Exponential(5.0)],
	...     routing=[[0.0, 0.0], [0.0, 0.0]],
	...     number_of_servers=[1, 1]
	... )

Nawr ail-rhedwn yr un system, gan ddweud wrth Ciw i ddefnyddio'r :code:`arrival_node_class` newydd.
Gwelwn bron yr un nifer o gwasanaethau yn digwydd yn Nod 1, ond mae'r cwsmeriaud a fydd wedi cael eu gwrthod nawr yn cael gwasanaethau yn Nod 2::

	>>> ciw.seed(1)
	>>> Q = ciw.Simulation(N, arrival_node_class=CustomArrivalNode)
	>>> Q.simulate_until_max_time(100)

	>>> service_nodes = [r.node for r in Q.get_all_records()]
	>>> Counter(service_nodes)
	Counter({1: 503, 2: 84})
