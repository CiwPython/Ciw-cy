.. _server-schedules:

======================================
Aseinio Amserlenni Gwaith i Weinyddion
======================================

Mae Ciw yn galluogi defnyddwyr i aseinio amserlenni gwaith cylchol i weinyddion ym mhob gorsaf gwasanaeth.
Gall esiampl o amserlen gwaith cylchol edrych fel hyn:

	+-------------------+---------+---------+---------+---------+---------+---------+
	|    Shift Times    |    0-40 |  40-100 | 100-120 | 120-180 | 180-220 | 220-250 |
	+-------------------+---------+---------+---------+---------+---------+---------+
	| Number of Servers |       2 |       3 |       1 |       2 |       4 |       0 | 
	+-------------------+---------+---------+---------+---------+---------+---------+

Mae'r amserlen hon yn gylchol, ac felly ar ôl y shifft olaf (220-250), mae'r amserlen yn dechrau eto gyda'r shifft (0-40). Cyfnod y cylchred yw 250.

Er mwyn ddiffinio'r amserlen gwaith hon, rhaid rhoi enw iddo.
Gadewch i ni ei alw'n :code:`fy_amserlen_arbennig_01`.

Yn y ffeil :code:`parameters.yml`, o dan :code:`Number_of_servers`, ar gyfer y nod priodol rhowch enw'r amserlen. Rhaid rhoi'r :code:`Cycle_length` hefyd.
Dangosir esiampl::

    Cycle_length: 250
    Number_of_servers:
      - 'fy_amserlen_arbennig_01'
      - 3

Y ffordd gyfatebol i ychwanegu hwn i'r geiriadur paramedrau yw trwy ychwanegu cyfnod y cylchred yn gyntaf::
    
    'Cycle_length':250

Ac o dan :code:`Number_of_servers` ychwanegwch enw'r amserlen::

    'Number_of_servers':['fy_amserlen_arbennig_01', 3]

Mae hwn yn dweud Ciw bydd nifer o weinyddion yn Nod 1 yn newid dros amser yn ôl yr amserlen gwaith :code:`fy_amserlen_arbennig_01`.

Nid yw'r amserlen wedi'i ddiffinio eto.
I ddiffinio'r amserlen gwaith, ychwanegwch y llinellau canlynol i ddiwedd y ffeil :code:`parameters.yml`::

    fy_amserlen_arbennig_01:
      - - 0
        - 2
      - - 40
        - 3
      - - 100
        - 1
      - - 120
        - 2
      - - 180
        - 4
      - - 220
        - 0

A'r ffordd gyfatebol yn y geiriadur paramedrau yw ychwanegu'r canlynol::

    'fy_amserlen_arbennig_01':[[0, 2], [40, 3], [100, 1], [120, 2], [180, 4], [220, 0]]

Fan hyn rydym yn dweud fe fydd yna 2 weinydd rhwng amseroedd 0 a 40, 3 rhwng amseroedd 40 a 100, ayyb. Mae'r shifft olaf yn dynodi 0 gweinydd rhwng amseroedd 220 a :code:`Cycle_length`, ac yna mae'r amserlen yn cylchu i'r dechrau.
Mae hwn yn diffinio'r amserlen gwaith yn llawn.

Noder:

- Os ddiffinnir mwy nag un amserlen gwaith, rhaid defnyddio'r un :code:`Cycle_length` ar gyfer y system gyfan.