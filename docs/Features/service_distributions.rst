.. _service-distributions:

===================================================
Dosraniadau Amseroedd Gwasanaeth a Rhwng-Dyfodiadau
===================================================

Ar hyn o bryd mae Ciw yn caniatáu'r dosraniadau canlynol ar gyfer amseroedd gwasanaeth a rhwng-dyfodiadau, yn ogystal â dosraniadau empirig a trwy fewnbynnu ffwythiant eich hun:

- :ref:`uniform_dist`
- :ref:`deterministic_dist`
- :ref:`triangular_dist`
- :ref:`exponential_dist`
- :ref:`gamma_dist`
- :ref:`lognormal_dist`
- :ref:`weibull_dist`
- :ref:`empirical_dist`
- :ref:`own_functions`


Gweler :ref:`custom-distributions` i weld sut allwch ddiffinio FfDT arwahanol ar gyfer amseroedd gwasanaeth.
Noder pan ddewisir paramedrau ar gyfer y dosraniadau yma, sicrhewch ni all samplo rhifau negatif.

.. _uniform_dist:

-------------------
Y Dosraniad Unffurf
-------------------

Samplwyd y dosraniad unffurf rhif ar hap rhwng dau rif `a` a `b`.
Yn y geiriagur paramedrau, mae'r cod isod yn diffinio dosraniad unffurf rhwng `4` a `9`::

    ['Uniform', 4.0, 9.0]




.. _deterministic_dist:

-------------------------
Y Dosraniad Penderfynedig
-------------------------

Nid yw'r dosraniad penderfynedig yn stocastig, a chynhyrchwyd yr un amser gwasanaeth dro ar ôl tro.
Yn y geiriagur paramedrau, mae'r cod isod yn diffinio dosraniad penderfynedig sy'n rhoi'r gwerth `18.2`::

    ['Deterministic', 18.2]




.. _triangular_dist:

---------------------
Y Dosraniad Trionglog
---------------------

Samplwyd y dosraniad trionglog rhif ar hap o FfDT parhaus sy'n codi'n llinol o'i werth isaf `is` i'w modd `modd`, a’n yna'n disgyn yn llinol i'w werth uchaf `uch`.
Yn y geiriagur paramedrau, mae'r cod isod yn diffinio dosraniad trionglog rhwng `2.1` a `7.6` gyda modd `3.4`::

    ['Triangular', 2.1, 7.6, 3.4]





.. _exponential_dist:

----------------------
Y Dosraniad Esbonyddol
----------------------

Samplwyd y dosraniad esbonyddol rhif ar hap o'r dosraniad esbonyddol negatif gyda chymedr `1 / lambda`.
Yn y geiriagur paramedrau, mae'r cod isod yn diffinio dosraniad esbonyddol gyda chymedr `0.2`::

    ['Exponential', 5]







.. _gamma_dist:

----------------
Y Dosraniad Gama
----------------

Samplwyd y dosraniad gama rhif ar hap o'r dosraniad gama gyda pharamedr siâp `alffa` a pharamedr raddfa `beta`.
Yn y geiriagur paramedrau, mae'r cod isod yn diffinio dosraniad gama gyda pharamedrau `alffa = 0.6` a `beta = 1.2`::

    ['Gamma', 0.6, 1.2]







.. _lognormal_dist:

---------------------
Y Dosraniad Lognormal
---------------------

Samplwyd y dosraniad gama rhif ar hap o log y dosraniad normal gyda chymedr `mu` a gwiriad safonol `sigma`.
Yn y geiriagur paramedrau, mae'r cod isod yn diffinio log y dosraniad normal gyda chymedr `4.5` a gwiriad safonol `2.0`::

    ['Lognormal', 4.5, 2.0]






.. _weibull_dist:

-------------------
Y Dosraniad Weibull
-------------------

Samplwyd y dosraniad Weibull rhif ar hap o'r dosraniad Weibull gyda pharamedr raddfa `alffa` a pharamedr siâp `beta`.
Yn y geiriagur paramedrau, mae'r cod isod yn diffinio dosraniad Weibull gyda pharamedrau `alffa = 0.9` a `beta = 0.8`::

    ['Weibull', 0.9, 0.8]





.. _empirical_dist:

-------------------
Dosraniadau Empirig
-------------------

Mae yna dau ddull o ddiffinio dosraniadau empirig yn Ciw, naill ai trwy fewnbynnu rhestr arsylwadau, neu trwy roi path i ffeil :code:`.csv` yn cynnwys yr arsylwadau:

Mewnbynnu rhestr arsylwadau::

    ['Empirical', [0.3, 0.3, 0.3, 0.4, 0.5, 0.6, 0.8, 0.9, 1.1, 1.1, 1.1, 1.1]]

Mewnbynnu path i ffeil :code:`.csv`::

    ['Empirical', '<path_i_ffeil>']





.. _own_functions:

----------------------
Mewnbynnu Ffwythiannau
----------------------

Mae Ciw yn gadael i ddefnyddwyr mewnbynnu ffwythiannau ei hun i gynhyrchu amseroedd gwasanaeth a rhwng-dyfodiadau. Gall wneud hyn trwy roi ffwythiant yn y ffordd ganlynol::

	['UserDefined', lambda : random.random()]
