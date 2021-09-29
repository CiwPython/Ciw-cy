.. _behaviour-nodes:

=============================
Sut i Gael Ymddygiad Pwrpasol
=============================

Gall cael ymddygiad pwrpasol gan ysgrifennu dosbarthiadau :code:`Node`, :code:`ArrivalNode`, :code:`Individual`, ac/neu :code:`Server` newydd, sy'n etifeddu o'r :code:`ciw.Node`, :code:`ciw.ArrivalNode`, :code:`ciw.Individual` ac :code:`ciw.Server` yn ôl eu trefn, sy'n cyflwyno ymddygiad newydd i mewn i'r system.
Y dosbarthaidau gall cael eu trosysgrifenn yw:

- :code:`Node`: y prif dosbarth ar gyfer cynrychioli gorsaf wasanaeth.
- :code:`ArrivalNode`: y dosbarth ar gyfer generadu unigolion newydd a'u trosglwyddo i :code:`Node` penodol.
- :code:`Individual`: dosbarth ar gyfer cynrychioli unigolion.
- :code:`Server`: dosbarth ar gyfer cynrychioli'r gweinyddion sy'n eistedd mewn gorsaf wasanaeth.

Gallwch defnyddio'r dosbarthau newydd hyn gyda'r dosbarth :code:`Simulation` gan ddefnyddio'r dadleuon :code:`node_class`, :code:`arrival_node_class`, :code:`individual_class`, a :code:`server_class`.
Mae'r dadleuon hyn yn cynryd dosbarth (nid gwrthrych), i'w ddefnyddio trwy gydol yr holl efelychiad.
Mae'r dadl :code:`node_class` hefyd yn gallu cymryd rhestr o dosbarthau, yn dynodi pa dosbarth i'w ddefnyddio ym mhob nod y rhwydwaith. Mae hwn yn galluogi gwahanol nodau yn ymddwyn mewn ffyrdd gwahanol iawn i'w gilydd.


LLyfrgell o Enghreifftiau
-------------------------

Dyma llyfrgell o enghreifftiau o ddefnydd hwn:

.. toctree::
   :maxdepth: 1
   
   custom_routing.rst
   custom_arrivals.rst
   custom_number_servers.rst
   ps_routing.rst