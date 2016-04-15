.. _dynamic-classes:

==========================
Dosbarthau Cwsmer Deinamig
==========================

Mae Ciw yn gadael i gwsmeriaid newid ei dosbarth cwsmer yn ôl tebygolrwydd ar ôl gorffen gwasanaeth. Hynny yw ar ôl gwasanaeth yn nod `k` fe fydd cwsmer o ddosbarth `i` yn dod yn gwsmer o ddosbarth `j` gyda thebygolrwydd `P(J=j | I=i, K=k)`. Mewnbynna'r tebygolrwyddau hyn trwy'r :code:`Class_change_matrices`.

Dangosir esiampl o matrics newid dosbarth ar gyfer nod isod:

+-----------------+
| Nod  1          |
+=====+=====+=====+
| 0.3 | 0.4 | 0.3 |
+-----+-----+-----+
| 0.1 | 0.9 | 0.0 |
+-----+-----+-----+
| 0.5 | 0.1 | 0.4 |
+-----+-----+-----+


+-----------------+
| Nod  2          |
+=====+=====+=====+
| 1.0 | 0.0 | 0.0 |
+-----+-----+-----+
| 0.4 | 0.5 | 0.1 |
+-----+-----+-----+
| 0.2 | 0.2 | 0.6 |
+-----+-----+-----+

Yn yr esiampl hon fydd cwsmer dosbarth 0 yn gorffen gwasanaeth yn nod 1 yn dod yn gwsmer dosbarth 0 gyda thebygolrwydd 0.3, yn dod yn gwsmer dosbarth 1 gyda thebygolrwydd 0.4, ac yn dod yn gwsmer dosbarth 2 gyda thebygolrwydd 0.3. Rhoddir matrics gwahanol ar gyfer cwsmeriaid yn gorffen gwasanaeth yn nod 2.

Mewnbynna hyn i'r model efelychiad trwy ychwanegu'r canlynol i'r geiriadur paramedrau::
    
    'Class_change_matrices': {'Node 0': [[0.3, 0.4, 0.3], [0.1, 0.9, 0.0], [0.5, 0.1, 0.4]], 'Node 1': [[1.0, 0.0, 0.0], [0.4, 0.5, 0.1], [0.2, 0.2, 0.6]]}

Mae hwn yn gyfatebol i ychwanegu'r cod canlynol i'r ffeil paramedrau::

    Class_change_matrices:
      Node 0:
      - - 0.3
        - 0.4
        - 0.3
      - - 0.1
        - 0.9
        - 0.0
      - - 0.5
        - 0.1
        - 0.4
      Node 1:
      - - 1.0
        - 0.0
        - 0.0
      - - 0.4
        - 0.5
        - 1.0
      - - 0.2
        - 0.2
        - 0.6

Heb ychwanegu'r cod hwn bydd y model yn cymryd yn ganiataol fod cwsmeriaid ddim yn newid dosbarth.