.. _server-schedules:

======================================
Aseinio Amserlenni Gwaith i Weinyddion
======================================

Mae Ciw yn galluogi defnyddwyr i aseinio amserlenni gwaith cylchol i weinyddion ym mhob gorsaf gwasanaeth.
Gall esiampl o amserlen gwaith cylchol edrych fel hyn:

	+--------------------+---------+---------+---------+---------+---------+---------+
	|  Amseroedd sifft   |    0-40 |  40-100 | 100-120 | 120-180 | 180-220 | 220-250 |
	+--------------------+---------+---------+---------+---------+---------+---------+
	| Nifer o weinyddion |       2 |       3 |       1 |       2 |       4 |       0 | 
	+--------------------+---------+---------+---------+---------+---------+---------+

Mae'r amserlen hon yn gylchol, ac felly ar ôl y shifft olaf (220-250), mae'r amserlen yn dechrau eto gyda'r shifft (0-40). Cyfnod y cylchred yw 250.

Er mwyn ddiffinio'r amserlen gwaith hon, rhaid rhoi enw iddo.
Gadewch i ni ei alw'n :code:`fy_amserlen_arbennig_01`.

Yn y ffeil :code:`parameters.yml`, o dan :code:`Number_of_servers`, ar gyfer y nod priodol rhowch enw'r amserlen.
Dangosir esiampl::

    Number_of_servers:
      - 'fy_amserlen_arbennig_01'
      - 3

Y ffordd gyfatebol i ychwanegu hwn i'r geiriadur paramedrau yw::

    'Number_of_servers':['fy_amserlen_arbennig_01', 3]

Mae hwn yn dweud Ciw bydd nifer o weinyddion yn Nod 1 yn newid dros amser yn ôl yr amserlen gwaith :code:`fy_amserlen_arbennig_01`.

Nid yw'r amserlen wedi'i ddiffinio eto.
I ddiffinio'r amserlen gwaith, ychwanegwch y llinellau canlynol i ddiwedd y ffeil :code:`parameters.yml`::

    fy_amserlen_arbennig_01:
      - - 40
        - 2
      - - 100
        - 3
      - - 120
        - 1
      - - 180
        - 2
      - - 220
        - 4
      - - 250
        - 0

A'r ffordd gyfatebol yn y geiriadur paramedrau yw ychwanegu'r canlynol::

    'my_special_schedule_01':[[40, 2], [100, 3], [120, 1], [180, 2], [220, 4], [250, 0]]

Fan hyn rydym yn dweud fe fydd yna 2 weinydd rhwng amseroedd 0 a 40, 3 rhwng amseroedd 40 a 100, ayyb.
Mae hwn yn diffinio'r amserlen gwaith yn llawn.