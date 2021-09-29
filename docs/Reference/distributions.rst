.. _refs-dists:

==================
Rhestr Dosraniadau
==================

Mae Ciw yn caniatáu nifer o ddosraniadau gwasanaeth a rhwng-dyfodiad parhaus, yn ogystal â dosraniadau empirig, amser dibynnol, dosraniadau a ddiffinnir gan y defnyddiwr, a dosraniadau arwahanol.
Wrth ddewis paramedrau ar gyfer y dosraniadau, sicrhewch ni samplwyd rhifau negatif.
Ar yn o bryd cynigir y dosraniadau canlynol:


- :ref:`uniform_dist`
- :ref:`deterministic_dist`
- :ref:`triangular_dist`
- :ref:`exponential_dist`
- :ref:`gamma_dist`
- :ref:`normal_dist`
- :ref:`lognormal_dist`
- :ref:`weibull_dist`
- :ref:`empirical_dist`
- :ref:`sequential_dist`
- :ref:`custom_pdf`
- :ref:`no_arrivals`



.. _uniform_dist:

-------------------
Y Dosraniad Unffurf
-------------------

Mae'r dosraniad unffurf yn samplu haprif rhwng dau rif `a` a `b`.
Ysgrifennwch ddosraniad unffurf rhwng `4` a `9`::

    ciw.dists.Uniform(4.0, 9.0)





.. _deterministic_dist:

-------------------------
Y Dosraniad Penderfynedig
-------------------------

Mae'r dosraniad penderfynedig yn ddi-stocastig, ac yn cynhyrchu'r un rhif dro ar ôl tro.
Ysgrifennwch ddosraniad penderfynedig sy'n rhoi'r gwerth `18.2` pob tro::

    ciw.dists.Deterministic(18.2)





.. _triangular_dist:

---------------------
Y Dosraniad Trionglog
---------------------

Mae'r dosraniad trionglog yn samplu o FfDT parhaus sy'n codi'n llinol o'i werth lleiaf `low` i'w werth moddol `mode`, ac yna'n disgyn yn llinol i'w gwerth mwyaf `high`.
Ysgrifennwch ddosraniad trionglog rhwng `2.1` a `7.6` gyda modd `3.4`::

    ciw.dists.Triangular(2.1, 3.4, 7.6)





.. _exponential_dist:

----------------------
Y Dosraniad Esbonyddol
----------------------

Mae'r dosraniad esbonyddol yn samplu haprif o'r dosraniad esbonyddol negatif gyda chymedr :math:`1/\lambda`.
Ysgrifennwch ddosraniad esbonyddol gyda chymedr `0.2`::

    ciw.dists.Exponential(5)





.. _gamma_dist:

----------------
Y Dosraniad Gama
----------------

Mae'r dosraniad gama yn samplu haprif o'r dosraniad gama gyda pharamedr siâp :math:`\alpha` a pharamedr graddfa :math:`\beta`.
Ysgrifennwch ddosraniad gama gyda pharamedrau :math:`\alpha = 0.6` a :math:`\beta = 1.2`::

    ciw.dists.Gamma(0.6, 1.2)





.. _normal_dist:

---------------------------
Y Dosraniad Normal Blaendor
---------------------------

Mae'r dosraniad normal blaendor yn samplu haprif o'r dosraniad normal gyda chymedr :math:`\mu` a gwyriad safonol :math:`\sigma`.
Mae'r dosraniad wedi'i blaendorri wrth 0, felly os samplir rhif negatif yna fe ail-samplir yr arsylwad yna nes samplir rhif positif.
Ysgrifennwch ddosraniad normal blaendor gyda pharamedrau :math:`\mu = 0.7` a :math:`\sigma = 0.4`::

    ciw.dists.Normal(0.7, 0.4)





.. _lognormal_dist:

---------------------
Y Dosraniad Lognormal
---------------------

Mae'r dosraniad lognormal yn samplu haprif o log y dosraniad normal gyda chymedr :math:`\mu` a gwyriad safonol :math:`\sigma`.
Ysgrifennwch ddosraniad lognormal, hynny yw log o'r dosraniad normal gyda :math:`\mu = 4.5` a :math:`\sigma = 2.0`::

    ciw.dists.Lognormal(4.5, 2.0)





.. _weibull_dist:

-------------------
Y Dosraniad Weibull
-------------------

Mae'r dosraniad Weibull yn samplu haprif o'r dosraniad Weibull gyda pharamedr graddfa :math:`\alpha` a pharamedr siâp :math:`\beta`.
Ysgrifennwch ddosraniad Weibull gyda :math:`\alpha = 0.9` a :math:`\beta = 0.8`::

    ciw.dists.Weibull(0.9, 0.8)





.. _empirical_dist:

-------------------
Dosraniadau Empirig
-------------------

Mae'r dosraniad empirig yn dewis gwerthoedd o rhestr ar hap.
Os yw arsylwadau yn ymddangos yn fwy aml yn y rhestr, byddant yn cael ei samplu'n fwy aml.
I fewnbynnu rhestr o arsylwadau::

    ciw.dists.Empirical([0.3, 0.3, 0.3, 0.4, 0.5, 0.6, 0.8, 0.9, 1.1, 1.1, 1.1, 1.1])






.. _sequential_dist:

-----------------------
Dosraniadau Dilyniannol
-----------------------

Mae dosraniad dilyniannol yn cymryd rhestr, ac yn rhoi'r arsylwad nesaf yn y rhestr yn ailadroddol dros amser.
Mae'r dosraniad yn gylchol, felly unwaith mae holl elfennau'r rhestr wedi'i samplu, mae'r dilyniant o werthoedd i'w samplu yn dechrau eto o ddechrau'r rhestr::

    ciw.dists.Sequential([0.1, 0.1, 0.2, 0.1, 0.3, 0.2])





.. _custom_pdf:

---------------------------
Ffwythiant Mas Tebygolrwydd
---------------------------

Mae Ciw yn gadael i ddefnyddwyr diffinio dosraniadau ffwythiant mas tebygolrwydd (FfMT neu PMF) eu hun.
Mae'r dosraniad yn samplu o set gwerthoedd lle mae gan bob gwerth tebygolrwydd penodol, hynny yw samplu’r gwrth :math:`x` gyda thebygolrwydd :math:`P(x)`.
Er enghraifft, os yw :math:`P(1.4) = 0.2`, :math:`P(1.7) = 0.5`, a :math:`P(1.9) = 0.3`, ysgrifennwch::

    ciw.dists.Pmf([1.4, 1.7, 1.9], [0.2, 0.5, 0.3])




.. _no_arrivals:

--------------
Dim Dyfodiadau
--------------

Os nad yw nod yn cael unrhyw ddyfodiadau o ryw ddosbarth cwsmer, yna gallwch fewnbynnu'r cod isod yn lle dosraniad::

    ciw.dists.NoArrivals()

Nodwch fod hwn ond yn ddilys ar gyfer dyfodiadau, peidiwch â'i ddefnyddio ar gyfer yr opsiwn :code:`service_distributions`.