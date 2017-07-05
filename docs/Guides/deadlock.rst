.. _detect-deadlock:

=====================
Sut i Ganfod Llwyrglo
=====================

Ffenomen yw llwyrglo lle mar holl symudiad a llif cwsmeriaid mewn rhwydwaith ciwio cyfyngedig yn dod i ben, oherwydd blocio cylchol.
Mae'r diagram isod yn dangos enghraifft, mae'r cwsmer yn y nod top wedi blocio i'r nod gwaelod, a'r cwsmer yn y nod gwaelod wedi blocio i'r nod top.
Mae'r blocio cylchol yma yn achosi holl symudiad naturiol i beidio.

.. image:: ../_static/2nodesindeadlock.svg
   :scale: 100 %
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
    ...    Arrival_distributions=[['Exponential', 6.0]],
    ...    Service_distributions=[['Exponential', 5.0]],
    ...    Transition_matrices=[[0.5]],
    ...    Number_of_servers=[1],
    ...    Queue_capacities=[3]
    ... )

Rhedeg nes cyrraedd llwyrglo::

    >>> import ciw
    >>> ciw.seed(1)
    >>> Q = ciw.Simulation(N, deadlock_detector='StateDigraph')
    >>> Q.simulate_until_deadlock()
    >>> Q.times_to_deadlock # doctest:+SKIP
    {((0, 0),): 0.94539784..., ((1, 0),): 0.92134933..., ((2, 0),): 0.68085451..., ((3, 0),): 0.56684471..., ((3, 1),): 0.0, ((4, 0),): 0.25332344...}

Fan hyn allweddau yn cyfateb a chyflyrau a chofnodwyd gan y traciwr cyflwr.



.. _state-trackers:

Sut i Osod Traciwr Cyflwr
=========================

Mae gan Ciw yr opsiwn i actifadu traciwr cyflwr (:code:`tracker`) er mwyn tracio cyflwr y system wrth iddo symud tuag at lwyrglo.
Y traciwr diofyn yw'r :code:`StateTracker` sy'n gwneud dim byd (heblaw bod yr efelychiad yn canfod llwyrglo, yna :code:`NaiveTracker` yw'r opsiwn diofyn).
Mae gan y tracwyr defnydd wrth efelychu nes cyrraedd llwyrglo, gan fod yr amser nes cyrraedd llwyrglo o bob cyflwr yn cael eu cofnodi.

Ar gyfer rhestr ac esboniad o bob traciwr cyflwr sydd gan Ciw, gwelwch :ref:`refs-statetrackers`.

Ystyriwch y ciw M/M/2/1 gyda dolen adborth.
Os defnyddir Traciwr Naïf disgwylir y cyflyrau canlynol: ((0, 0)), ((1, 0)), ((2, 0)), ((3, 0)), ((2, 1)), ((1, 2)).
Yn efelychu nes cyrraedd llwyrglo, bydd y geiriadur :code:`times_to_deadlock` yn cynnwys is-set o'r cyflyrau yma fel allweddau::

    >>> import ciw
    >>> N = ciw.create_network(
    ...    Arrival_distributions=[['Exponential', 6.0]],
    ...    Service_distributions=[['Exponential', 5.0]],
    ...    Transition_matrices=[[0.5]],
    ...    Number_of_servers=[2],
    ...    Queue_capacities=[1]
    ... )

    >>> ciw.seed(1)
    >>> Q = ciw.Simulation(N, deadlock_detector='StateDigraph', tracker='Naive')
    >>> Q.simulate_until_deadlock()
    >>> Q.times_to_deadlock # doctest:+SKIP
    {((0, 0),): 1.3354..., ((1, 0),): 1.3113..., ((1, 2),): 0.0, ((2, 0),): 1.0708..., ((2, 1),): 0.9353..., ((3, 0),): 0.9568...}



Os defnyddir Traciwr Matrics disgwylir y cyflyrau canlynol: ((()), (0)), ((()), (1)), ((()), (2)), ((()), (3)), (((1)), (3)), (((1, 2)), (3)).

    >>> ciw.seed(1)
    >>> Q = ciw.Simulation(N, deadlock_detector='StateDigraph', tracker='Matrix')
    >>> Q.simulate_until_deadlock()
    >>> Q.times_to_deadlock # doctest:+SKIP
    {((((),),), (0,)): 1.3354..., ((((),),), (1,)): 1.3113..., ((((),),), (2,)): 1.0708..., ((((),),), (3,)): 0.9568..., ((((1,),),), (3,)): 0.9353..., ((((1, 2),),), (3,)): 0.0}


Nodwch yn yr achos syml yma, mae'r Tracwyr Naïf a Matrics yn cyfateb a'r un cyflyrau.
Mewn achosion arall, lle gall cwsmeriaid cael eu blocio mewn gwahanol drefnau ac i lefydd gwahanol, yna gall y ddau tracwyr tracio cyflyrau system wahanol.
