.. _behaviour-nodes:

=============================
Sut i Gael Ymddygiad Pwrpasol
=============================

Gall cael ymddygiad pwrpasol gan ysgrifennu dosbarthiadau :code:`Node` a :code:`ArrivalNode` newydd, sy'n etifeddu o'r dosbarthau :code:`ciw.Node` d :code:`ciw.ArrivalNode` gwreiddiol, ac sy'n cyflwyno ymddygiad newydd i'r system.
Y dosbarthau a gall cael eu drosysgrifio yw:

- :code:`Node`: y prif ddosbarth nod sy'n cynrychioli gorsaf gwasanaeth.
- :code:`ArrivalNode`: y dosbarth nod a ddefnyddir i eneradu unigolion a'u drosglwyddo i :code:`Node` penodol.

Gall ddefnyddio'r dosbarthau Node ac Arrival Node newydd hyn yn y dosbarth Simulation gan ddefnyddio'r allweddeiriau :code:`node_class` a :code:`arrival_node_class`.

Ystyriwch y rhwydwaith dau nod canlynol, lle mae dyfodiadau ond yn digwydd yn y nod cyntaf, ac mae yna gynhwysedd ciwio o 10.
Mae'r ail nod yn segur yn y sefyllfa yma::

	>>> import ciw
	>>> from collections import Counter

	>>> N = ciw.create_network(
	...     Arrival_distributions=[['Exponential', 6.0], 'NoArrivals'],
	...     Service_distributions=[['Exponential', 5.0], ['Exponential', 5.0]],
	...     Transition_matrices=[[0.0, 0.0], [0.0, 0.0]],
	...     Number_of_servers=[1, 1],
	...     Queue_capacities=[10, 'Inf']
	... )

Nawr rhedwn yr efelychiad am 100 uned amser, a gwelwn fod 484 gwasanaeth wedi digwydd wrth y nod cyntaf, a dim wrth yr ail nod::

	>>> ciw.seed(1)
	>>> Q = ciw.Simulation(N)
	>>> Q.simulate_until_max_time(100)

	>>> service_nodes = [r.node for r in Q.get_all_records()]
	>>> Counter(service_nodes)
	Counter({1: 484})

Nawr crëwn :code:`CustomArrivalNode` newydd felly anfonir unrhyw gwsmeriaid sy'n cyrraedd pan mae'r gan y nod cyntaf 10 neu fwy o gwsmeriaid i'r ail nod.
Yn gyntaf crëwch y :code:`CustomArrivalNode` sy'n etifeddu o'r :code:`ciw.ArrivalNode`, a throsysgrifwch y dull :code:`send_individual`::

	>>> class CustomArrivalNode(ciw.ArrivalNode):
	...     def send_individual(self, next_node, next_individual):
	...         """
	...         Sends the next_individual to the next_node
	...         """
	...         self.number_accepted_individuals += 1
	...         if len(next_node.all_individuals) <= 10:
	...             next_node.accept(next_individual, self.next_event_date)
	...         else:
	...             self.simulation.nodes[2].accept(next_individual, self.next_event_date)

I redeg yr un system, rhaid i ni hepgor yr allweddair :code:`'Queue_capacities'` felly ni wrthodir cwsmeriaid cyn cyrraedd y dull :code:`send_individual`::

	>>> N = ciw.create_network(
	...     Arrival_distributions=[['Exponential', 6.0], 'NoArrivals'],
	...     Service_distributions=[['Exponential', 5.0], ['Exponential', 5.0]],
	...     Transition_matrices=[[0.0, 0.0], [0.0, 0.0]],
	...     Number_of_servers=[1, 1]
	... )

Nawr fe ail-rhedwn y system, yn dweud wrth Ciw am ddefnyddio'r :code:`arrival_node_class` newydd.
Gwelwn fod yr un nifer o wasanaethau wedi digwydd wrth Nod 1, ond nawr mae'r cwsmeriaid a chafodd eu gwrthod nawr yn cael gwasanaethau wrth Nod 2::

	>>> ciw.seed(1)
	>>> Q = ciw.Simulation(N, arrival_node_class=CustomArrivalNode)
	>>> Q.simulate_until_max_time(100)

	>>> service_nodes = [r.node for r in Q.get_all_records()]
	>>> Counter(service_nodes)
	Counter({1: 484, 2: 85})
