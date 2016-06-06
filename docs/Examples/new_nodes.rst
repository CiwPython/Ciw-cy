.. _new_nodes:

==================================================
Enghraifft - Modelu ymddygiad gan ddefnyddio nodau
==================================================

Fel engrhaifft o hyblygrwydd Ciw, fe allwch addasu'r trosglwyddiadau unigolion gan creu nodau newydd: 

- :code:`Node`: y prif dosbarth nod sy'n cyfateb a ganolfan gwasanaeth.
- :code:`ArrivalNode`: y dosbarth node sy'n generadu unigolion ac yn eu anfon i'r :code:`Node` priodol.

Ystyriwch sefyllfa lle mae unigolyn ond yn ymuno a/neu ailymuno a ciw gyda un gweinydd of oes llai na :code:`trothwy` o unigolion yna yn barod::

    >>> import ciw
    >>> threshold = 10
    >>> class ThresholdNode(ciw.Node):
    ...    def next_node(self, customer_class):
    ...        """Yn trosgrifio'r method next_node"""
    ...        if len(self.simulation.nodes[1].individuals) < threshold:
    ...            return self.simulation.nodes[1]
    ...        return self.simulation.nodes[-1]

    >>> class ThresholdArrivalNode(ciw.ArrivalNode):
    ...     def release_individual(self, next_node, next_individual):
    ...         """Yn trosgrifio'r method release_individual"""
    ...         if len(next_node.individuals) < threshold:
    ...             self.send_individual(next_node, next_individual)
    ...         else:
    ...             self.record_rejection(next_node)

Fe allwn defnyddio'r nodau newydd yma i adaeladu'r efelychiad::

    >>> params = {
    ...  'Arrival_distributions': [['Exponential', 5.0]],
    ...  'Service_distributions': [['Exponential', 10.0]],
    ...  'Transition_matrices': [[0.5]],
    ...  'Number_of_servers': [1]
    ...  }

Gadewch i ni cymharu'r nifer macsimwm o unigolion yn y ciw ar unrhyw adeg o'r efelychiad yn defnyddio'r nodau newydd yma ac hefyd y nodau diofyn::

    >>> network = ciw.create_network(params)

    >>> default_Q = ciw.Simulation(network)
    >>> default_Q.simulate_until_max_time(1000)
    >>> default_recs = default_Q.get_all_records()
    >>> default_max_length = max([row.queue_size_at_arrival for row in default_recs] +
    ...                          [row.queue_size_at_departure for row in default_recs])
    >>> default_max_length  # doctest: +SKIP
    108


    >>> threshold_Q = ciw.Simulation(network,
    ...                              node_class=ThresholdNode,
    ...                              arrival_node_class=ThresholdArrivalNode)
    >>> threshold_Q.simulate_until_max_time(1000)
    >>> threshold_recs = threshold_Q.get_all_records()
    >>> threshold_max_length = max([row.queue_size_at_arrival for row in threshold_recs] +
    ...                            [row.queue_size_at_departure for row in threshold_recs])
    >>> threshold_max_length
    9

    >>> threshold_max_length <= default_max_length
    True
