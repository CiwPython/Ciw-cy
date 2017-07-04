.. _refs-dists:

==================
Rhestr Dosraniadau
==================

Mae Ciw yn caniatáu nifer o dosraniadau gwasanaeth a rhwng-dyfodiad parhaus, yn ogsytal a dosraniadau empirig, amser dibynnol, dosraniadau a ddiffinir gan y defnyddiwr, a dosranidau arwahanol.
Pan yn dewis paramedrau ar gyfer y dosraniadau, sicrhwech ni samplwyd rhifau negatif.
Ar yn o bryd cynnigir y dosraniadau canlynol:


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
- :ref:`own_functions`
- :ref:`time_dependent`
- :ref:`no_arrivals`



.. _uniform_dist:

--------------------
Y Dosraniad Unffurdd
--------------------

Mae'r dosraniad unffurf yn samplu haprif rhwng dau rhif `a` a `b`.
Ysgrifennwch dosraniad unffurf rhwng `4` a `9`::

    ['Uniform', 4.0, 9.0]





.. _deterministic_dist:

-------------------------
Y Dosraniad Penderfynedig
-------------------------

Mae'r dosraniad penderfynedig yn ddi-stocastig, ac yn cynhyrchu'r un rhif dro ar ôl tro.
Ysgrifennwch dosraniad penderfynedig sy'n rhoi'r gwerth `18.2` pob tro::

    ['Deterministic', 18.2]





.. _triangular_dist:

---------------------
Y Dosraniad Trionglog
---------------------

Mae'r dosraniad trionglog yn samplu o ffdt parhaus sy'n codi'n llinol o'i werth minimwn `low` i'w werth moddol `mode`, ac yna'n disgyn yn llinol i'w gwerth mwyaf `high`.
Ysgrifennwch dosraniad trionglog rhwng `2.1` a `7.6` gyda modd `3.4`::

    ['Triangular', 2.1, 7.6, 3.4]





.. _exponential_dist:

----------------------
Y Dosraniad Esbonyddol
----------------------

Mae'r dosraniad esbonyddol yn samplu haprif o'r dosraniad esbonyddol negatif gyda cymedr :math:`1/\lambda`.
Ysgrifennwch dosraniad esbonyddol gyda cymedr `0.2`::

    ['Exponential', 5]





.. _gamma_dist:

----------------
Y Dosraniad Gama
----------------

Mae'r dosraniad gama yn samplu haprif o'r dosraniad gama gyda paramedr siâp :math:`\alpha` a paramedr graddfa :math:`\beta`.
Ysgrifennwch dosraniad gama gyda paramedrau :math:`\alpha = 0.6` a :math:`\beta = 1.2`::

    ['Gamma', 0.6, 1.2]





.. _normal_dist:

---------------------------
Y Dosraniad Normal Blaendor
---------------------------

Mae'r dosraniad normal blaendor yn samplu haprif o'r dosraniad normal gyda cymedr :math:`\mu` a gwyriad safonol :math:`\sigma`.
Mae'r dosraniad wedi'i blaendorri wrth 0, felly os samplir rhif negatif yna fe ail-samplir yr arsylwad yna nes samplir rhif positif.
Ysgrifennwch dosraniad normal blaendor gyda paramedrau :math:`\mu = 0.7` a :math:`\sigma = 0.4`::

    ['Normal', 0.7, 0.4]





.. _lognormal_dist:

---------------------
Y Dosraniad Lognormal
---------------------

Mae'r dosraniad lognormal yn samplu haprif o log y dosraniad normal gyda cymedr :math:`\mu` a gwyriad safonol :math:`\sigma`.
Ysgrifennwch dosraniad lognormal, hynny yw log o'r dosraniad normal gyda :math:`\mu = 4.5` and :math:`\sigma = 2.0`::

    ['Lognormal', 4.5, 2.0]





.. _weibull_dist:

-------------------
Y Dosraniad Weibull
-------------------

Mae'r dosraniad Weibull yn samplu haprif o'r dosraniad Weibull gyda paramedr graddfa :math:`\alpha` a paramedr siâp :math:`\beta`.
Ysgrifennwch dosraniad Weibull gyda :math:`\alpha = 0.9` a :math:`\beta = 0.8`::

    ['Weibull', 0.9, 0.8]





.. _empirical_dist:

-------------------
Dosraniadau Empirig
-------------------

Mae yna dau dull o ddiffinio dosraniadau empirig yn Ciw, naill ai trwy mewnbynnu arsylwadau, neu trwy rhoi'r path i ffeil :code:`.csv` sy'n cynnwys yr alsylwadau:

I mewnbynnu rhestr o arsylwadau::

    ['Empirical', [0.3, 0.3, 0.3, 0.4, 0.5, 0.6, 0.8, 0.9, 1.1, 1.1, 1.1, 1.1]]

I mewnbynnu path i ffeil :code:`.csv`::

    ['Empirical', '<path_to_file>']





.. _sequential_dist:

-----------------------
Dosraniadau Dilyniannol
-----------------------

Mae dosraniad dilyniannol yn cymryd rhestr, a yn rhoi'r arsylwad nesaf yn y rhestr yn ailadroddol dros amser.
Mae'r dosraniad yn cylchol, felly unwaith mae holl elfennau'r rhestr wedi'i samplu, mae'r dilyniant o gwerthoedd i'w samplu yn dechrau eto o dechrau'r rhestr::

    ['Sequential', [0.1, 0.1, 0.2, 0.1, 0.3, 0.2]]





.. _custom_pdf:

---------------------
Dosraniadau Arwahanol
---------------------

Mae Ciw yn gadael i ddefnyddwyr diffinio dosraniadau arwahanol eu hun.
Mae'r dosraniad yn samplu o set gwerthoedd lle mae gan pob gwerth tebygolrwydd penodol, hynny yw samply'r gwrth :math:`x` gyda tebygolrwydd :math:`P(x)`.
Er enghraifft, os yw :math:`P(1.4) = 0.2`, :math:`P(1.7) = 0.5`, a :math:`P(1.9) = 0.3`, ysgrifennwch::

    ['Custom', [1.4, 1.7, 1.9], [0.2, 0.5, 0.3]]






.. _own_functions:

----------------------------------------
Dosraniadau a Ddiffinir Gan y Defnyddiwr
----------------------------------------

Mae Ciw yn caniatáu i ddefnyddwyr mewnbynnu ffwythiannau eu hyn i generadu amseroedd gwasanaeth a rhwng-dyfodiad.
I bwydo mewn ffwythiant, ysgrifennwch::

	['UserDefined', random.random]





.. _time_dependent:

--------------------------
Dosraniadau Amser Dibynnol
--------------------------

Yn debyg i ychwanegu ffwythiannau :code:`UserDefined`, mae Ciw yn caniatáu ffwythiannau amser dibynnol.
Ffwythiannau lambda yw rhain sy'n cymryd paramedr amser.
Mae Ciw yn defnyddio amser presennol yr efelychiad i samlu amseroess o'r ffwythiant yma::

    ['TimeDependent', time_dependent_function]





.. _no_arrivals:

--------------
Dim Dyfodiadau
--------------

Os nad yw nod yn cael unrhyw dyfodiadau o rhyw dosbarth cwsmer, yna gallwch mewnbynnu'r cod isod yn lle dosraniad::

    'NoArrivals'

Nodwch diffig bracedu sgwâr yma.
Hefyd nodwch fod hwn ond yn ddilys ar gyfer dyfodiadau, peidiwch a'i ddefnyddio ar gyfer yr opsiwn :code:`Service_distributions`.