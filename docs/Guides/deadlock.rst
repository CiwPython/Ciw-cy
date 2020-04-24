.. _detect-deadlock:

=====================
Sut i Ganfod Llwyrglo
=====================

Ffenomen yw llwyrglo lle mar holl symudiad a llif cwsmeriaid mewn rhwydwaith ciwio cyfyngedig yn dod i ben, oherwydd blocio cylchol.
Mae'r diagram isod yn dangos enghraifft, mae'r cwsmer yn y nod top wedi blocio i'r nod gwaelod, a'r cwsmer yn y nod gwaelod wedi blocio i'r nod top.
Mae'r blocio cylchol yma yn achosi holl symudiad naturiol i beidio.

.. image:: ../_static/2nodesindeadlock.svg
   :alt: Rhwydwaith ciwio 2 node mewn llwyrglo.
   :align: center

Mae gan Ciw y gallu i ganfod llwyrglo.
Gyda Ciw, fe all efelychu rhwydwaith ciwio nes cyrraedd llwyrglo.
Yna mae Ciw yn cofnodi'r amser nes cyrraedd llwyrglo o bob cyflwr.
(Gwelwch y ddogfennaeth ar :ref:`tracwyr cyflwr <state-trackers>`.)

I fanteisio ar y nodwedd yma, gosodwch y ddadl :code:`deadlock_detection` i un o’r dulliau canfod llwyrglo wrth greu gwrthrych Simulation.
Ar hyn o bryd yr unig ddull yw :code:`'StateDigraph'`.
Yna defnyddiwch y dull :code:`simulate_until_deadlock`.
Mae'r briodwedd :code:`times_to_deadlock` yn cynnwys yr amseroedd nes cyrraedd llwyrglo o bob cyflwr.

Ystyriwch y ciw :ref:`M/M/1/3 <kendall-notation>` lle mae gan gwsmeriaid tebygolrwydd 0.5 o ail-ymuno a'r ciw ar ôl gwasanaeth.
Os yw'r ciw yn llawn yna caiff y cwsmer yn ei flocio, felly mae'r system yn cyrraedd llwyrglo.

Paramedrau::

    >>> import ciw
    >>> N = ciw.create_network(
    ...    arrival_distributions=[ciw.dists.Exponential(6.0)],
    ...    service_distributions=[ciw.dists.Exponential(5.0)],
    ...    routing=[[0.5]],
    ...    number_of_servers=[1],
    ...    queue_capacities=[3]
    ... )

Rhedeg nes cyrraedd llwyrglo (gan ddefnyddio gwrthrych :code:`ciw.trackers.NaiveBlocking`)::

    >>> import ciw
    >>> ciw.seed(1)
    >>> Q = ciw.Simulation(N,
    ...     deadlock_detector=ciw.deadlock.StateDigraph(),
    ...     tracker=ciw.trackers.NaiveBlocking()
    ... )
    >>> Q.simulate_until_deadlock()
    >>> Q.times_to_deadlock # doctest:+SKIP
    {((0, 0),): 0.94539784..., ((1, 0),): 0.92134933..., ((2, 0),): 0.68085451..., ((3, 0),): 0.56684471..., ((3, 1),): 0.0, ((4, 0),): 0.25332344...}

Fan hyn allweddau yn cyfateb a chyflyrau a chofnodwyd gan y traciwr cyflwr. Nodwch, er mwyn i :code:`times_to_deadlock` fod yn ystyrlon, angen defnyddio traciwr cyflwr.

