.. _process-based:

=======================================================
Sut i Ddiffinio Trosglwyddiadau wedi Seilio ar Brosesau
=======================================================

Mae gan Ciw y gallu i rhedeg efelychiadau wedi seilio ar brosesau (process-based). Mae hwn yn golygu fod taith cyfan cwsmer wedi'i pendrefynnu y dechrau, ac nid yw wedi'i penderfynnu gan tebygolrwyddau wrth iddynt teithio trwy'r rhwydwaith.
Mae hwn yn galluogi i teithiau cael ei penderfynnu gan hanes unigolyn, er enghraifft, ailadrodd nodau nifer penodol o weithiau.

Mae taith cyfan cwsmer wedi'i penderfynnu ar y dechrau, wedi'i generadu gan ffwythiant taith, sy'n cymryd i mewn unigolyn ac yn allbynnu taith, sef rhestr o trefn y nodau.
Er enghraifft::

    >>> def routing_function(ind):
    ...     return [1, 2, 2, 1]

Mae hwn yn cymryd unigolyn yn Nod 1 ac yn ei rhoi'r taith [1, 2, 2, 1]. Yn ar ôl gwasanaeth yn Nod 1 anfonnir yr unigolyn i Nod 2, yna nôl i Nod 2, yna nôl i Nod 1, cyn gadael y system. Nid yw sicrhau ailadrodd y nodau fel hyn yn bosib mewn system wedi'i seilio ar tebygolrwyddau yn unig.

Er mwyn defnyddio hwn, rydym yn amnewid y matrics trosglwyddo gyda rhestr o'r ffwythiannau taith hyn i defnyddio ym mhob pwynt dechrau. Er enghraifft::

    >>> import ciw
    
    >>> def repeating_route(ind):
    ...     return [1, 1, 1]

    >>> N = ciw.create_network(
    ...     arrival_distributions=[ciw.dists.Exponential(1)],
    ...     service_distributions=[ciw.dists.Exponential(2)],
    ...     number_of_servers=[1], 
    ...     routing=[repeating_route]
    ... )

Fan hyn mae cwsmeriaid yn dyfodi wrth Nod 1, yn cael gwasanaeth yna, ac yna yn ailadrodd hyn dwywaith cyn gadael y system.

Gadewch i ni rhedeg hyn i weld teithiau rheini sydd wedi gadael y system.

    >>> ciw.seed(0)
    >>> Q = ciw.Simulation(N)
    >>> Q.simulate_until_max_time(100.0)

    >>> inds = Q.nodes[-1].all_individuals # Gafael ym mhob unigolyn yn y nod ola
    >>> set([tuple(dr.node for dr in ind.data_records) for ind in inds]) # Gafael ym mhob taith yr unigolion hyn
    {(1, 1, 1)}

Nawr gwelwn bod pob unigolyn sydd wedi gadael y system, hynny yw yr unigolion sydd wedi cwpla eu taith, wedi ailadrodd gwasanaeth yn Nod 1 tait gwaith.

        
Sylw Pwysig
-----------

**Sut mae'n gwithio:** Gallwch meddwl am hwn fel, pan mae unigolyn yn cyrraedd ei nod cyntaf, yn seiliedig ar yr :code:`arrival_distributions`, aseinir taith y dylai dechrau wrth y nod hyn. Bydd hwn yn sicrhau bod y nod cyntaf y mae'r unigolyn yn cyrraedd yr un peth â nod cyntaf y taith a aseinir.

Os nad yw hwn yn digwydd bydd y gwall :code:`'Individual process route sent to wrong node'` yn codi.

*Gwnewch yn siwr bod y ffwythiant taith ar gyfer Node* :math:`i` *yn rhoi teithiau sy'n dechrau gyda Nod* :math`i`.


Enghraifft pellach
------------------

Gall y ffwythiannau taith bod mor gymleth a sydd angen. Maent yn cymryd unigolyn, ac felly'n gallu defnyddio unrhyw priodwedd yr unigolyn hynn wrth penderfynnu ar taith (gan gynnwys ei :code:`customer_class`).

Crëwn rhwydwaith gyda tri nod a'r taith canlynol:

* Ar gyfer cwsmeriaid yn dyfodi wrth Nod 1:

  * os oes gan yr unigolyn yna :code:`id_number` sy'n eilrif, ailadrodd Nod 1 dwywaith, yna gadael.

  * fel arall teithio o Nod 1 i Nod 2 i Nod 3 ac yna gadael.
  
* Mae gan dyfodiadau wrth Nod 2:

  * siawn 50% o teithio i Nod 3, yna gadael.

  * siawn 50% o teithio i Nod 1, yna gadael.

* Does dim dyfodiadau wrth Nod 3.

Ar gyfer hwn bydd angen dau ffwythiant taith: :code:`routing_function_Node_1`, :code:`routing_function_Node_2`::

    >>> def routing_function_Node_1(ind):
    ...     if ind.id_number % 2 == 0:
    ...         return [1, 1, 1]
    ...     return [1, 2, 3]

    >>> import random
    >>> def routing_function_Node_2(ind):
    ...     if random.random() <= 0.5:
    ...         return [2, 3]
    ...     return [2, 1]

Oherwydd nad oes dyfodiadau yn Nod 3, ni fydd cwsmer yn cael taith wedi aseinio iddynt yna. Ond, rhaid defnyddio'r ffwythiant deiliad lle :code:`ciw.no_routing` i adlewyrchu hyn::

    >>> N = ciw.create_network(
    ...     arrival_distributions=[ciw.dists.Exponential(1),
    ...                            ciw.dists.Deterministic(1),
    ...                            ciw.dists.NoArrivals()],
    ...     service_distributions=[ciw.dists.Exponential(2),
    ...                            ciw.dists.Exponential(2),
    ...                            ciw.dists.Exponential(2)],
    ...     number_of_servers=[1,1,1],
    ...     routing=[routing_function_Node_1,
    ...              routing_function_Node_2,
    ...              ciw.no_routing]
    ... )
