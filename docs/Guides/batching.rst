.. _batch-arrivals:

=========================
Sut i Osod Swp-Dyfodiadau
=========================

Mae Ciw yn caniatáu swp-dyfodiadau, hynny yw mwy nag un cwsmer yn cyrraedd ar yr un pryd.
Gallwch weithredu hwn gan ddefnyddio :code:`Batching_distributions`.
Yn debyg i :code:`Arrival_distributions` a :code:`Service_distributions`, mae hwn yn cymryd dosraniadau ar gyfer pob nod a dosbarth cwsmer a fydd yn samplu maint y swp.
Ond dosraniadau arwahanol a chaniateir, dosraniadau a samplwyd cyfanrifau.

Dangoswn esiampl::

    >>> import ciw
    >>> N = ciw.create_network(
    ...     Arrival_distributions=[['Deterministic', 18.5]],
    ...     Service_distributions=[['Deterministic', 3.0]],
    ...     Batching_distributions=[['Deterministic', 3]],
    ...     Number_of_servers=[1]
    ... )

Os efelychir y system am 30 uned amser, ond un dyfodiad a ddigwyddir.
Fodd bynnag, bydd 3 cwsmer yn cyrraedd ar yr un pryd.
Oherwydd ond un gweinydd sydd, bydd rhaid i ddau o'r cwsmeriaid yma aros::

    >>> Q = ciw.Simulation(N)
    >>> Q.simulate_until_max_time(30.0)
    >>> recs = Q.get_all_records()

    >>> [r.arrival_date for r in recs]
    [18.5, 18.5, 18.5]
    >>> [r.waiting_time for r in recs]
    [0.0, 3.0, 6.0]

Yn union fel dosraniadau rhwng-dyfodiad a gwasanaeth, gall diffinio dosraniadau sypiau ar gyfer nifer o nodau a nifer o ddosbarthau cwsmer, gan ddefnyddio rhestrau a geiriaduron::

    Batching_distributions={
        'Class 0': [['Deterministic', 3],
                    ['Deterministic', 1]],
        'Class 1': [['Deterministic', 2],
                    ['Deterministic', 2]]},

Nodwch:
  + *Ond dosraniadau arwahanol gallwch ddefnyddio,* ar hyn o bryd rhain yw:
     + :code:`Deterministic`
     + :code:`Empirical`
     + :code:`Custom`
     + :code:`Sequential`
  + Os hepgorwyd yr allweddair :code:`Batching_distributions` ni fyd unrhyw swp-dyfodi. Hynny yw ond un cwsmer bydd yn cyrraedd pob tro. Mae hwn yn cyfateb i :code:`['Deterministic', 1]`.
  + Os oes angen swp-dyfodiadau ar rhai nodau/dosbarthau cwsmer, ond fod angen swp-dyfodiadau ar rai, defnyddiwch :code:`['Deterministic', 1]`.
  + Fe all swp-dyfodiadau arwain at :ref:`digwyddiadau cydamserol <simultaneous_events>`, cymerwch ofal.
