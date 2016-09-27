.. _server-schedules:

=============================
Amserlenni Gwaith Gweinyddion
=============================

Mae Ciw yn galluogi defnyddwyr i aseinio amserlenni gwaith cylchol i weinyddion ym mhob gorsaf gwasanaeth.
Gall esiampl o amserlen gwaith cylchol edrych fel hyn:

	+--------------------+---------+---------+---------+---------+---------+---------+
	|  Amseroedd sifft   |    0-40 |  40-100 | 100-120 | 120-180 | 180-220 | 220-250 |
	+--------------------+---------+---------+---------+---------+---------+---------+
	| Nifer o weinyddion |       2 |       3 |       1 |       2 |       4 |       0 | 
	+--------------------+---------+---------+---------+---------+---------+---------+

Mae'r amserlen hon yn gylchol, ac felly ar ôl y shifft olaf (220-250), mae'r amserlen yn dechrau eto gyda'r shifft (0-40). Cyfnod y cylchred yw 250. Gadewch i ni alw'r amserlen hon yn :code:`fy_amserlen_arbennig_01`. Rydym yn diffinio'r amserlen yn y geiriadur paramedrau fel y dangosir::

    'Number_of_servers': ['fy_amserlen_arbennig_01', 3]

Fan hyn rydym yn dweud fe fydd yna 2 weinydd rhwng amseroedd 0 a 40, 3 rhwng amseroedd 40 a 100, ayyb.
Mae hwn yn diffinio'r amserlen gwaith yn llawn.

Yna mae'n rhaid i ni ddweud wrth Ciw pa nod sy'n defnyddio'r amserlen yma. Mae hwn yn dod o dan adran :code:`Number_of_servers` y geiriadur paramedrau. Yn syml, ychwanegwch enw'r amserlen yn lle'r cyfanrif arferol. Mae'r enghraifft isod yn dangos rhwydwaith dau nod, y cyntaf yn defnyddio'r amserlen uchod, a'r ail gyda 3 gweinydd statig::

    'Number_of_servers':['fy_amserlen_arbennig_01', 3]

**Noder fod ar hyn o bryd nid yw amserlenni gwaith a nifer anfeidraidd o weinyddion yn gweithio gyda'i gilydd**, ac felly ni allwch ychwanegu nifer anfeidraidd o weinyddion o fewn amserlen gwaith.

Y ffordd gyfatebol i ychwanegu hwn i'r ffeil paramedrau yw::

    Number_of_servers:
      - 'fy_amserlen_arbennig_01'
      - 3

Yn y ffeil :code:`parameters.yml`, o dan :code:`Number_of_servers`, ar gyfer y nod priodol rhowch enw'r amserlen.
Dangosir esiampl::

    'Number_of_servers':['fy_amserlen_arbennig_01', 3]

Y ffordd gyfatebol i ychwanegu hwn i'r geiriadur paramedrau yw::

    Number_of_servers:
      - 'fy_amserlen_arbennig_01'
      - 3
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


Rhagdarfiadau
-------------

Pan mae gweinydd angen mynd oddi ar ddyletswydd yng nghanol gwasanaeth cwsmer, mae yna dau opsiwn o beth gall ddigwydd.

+ Yn ystod amserlen rhagdarfiedig, fe fydd gweinydd yn stopio ar unwaith ac yn gadael. Pan mae gweinyddion newydd yn dod ar ddyletswydd fe fydden nhw'n blaenoriaethu'r cwsmeriaid a gafodd ei darfu. Ond mae amser gwasanaeth y cwsmeriaid yma yn cael ei ail-samplu. Felly, mae cwsmer sy'n dechrau gwasanaeth ar amser 5 i fod i gael amser gwasanaeth o 4, dylai orffen ar amser 9. Ond mae ei gweinydd yn mynd oddi ar ddyletswydd ar amser 7. Mae gweinydd arall yn ail-ddechrau ei wasanaeth ar amser 10, ac yn ail-samplu ei amser gwasanaeth, y tro yma dylai'r gwasanaeth par am 8 uned amser. Felly mae'r cwsmer yn gorffen gwasanaeth am amser 18. Yn y cofnodion, caiff hyn ei recordio fel cyfanswm amser gwasanaeth o 13, gan fod y gwasanaeth yn dechrau am amser 5 ac yn gorffen am amser 18.

+ Yn ystod amserlen anrhagdarfiedig, nid yw gwasanaethau cwsmeriaid yn cael ei darfu. Felly, mae gweinydd yn gorffen gwasanaeth y cwsmer presennol cyn diflannu. Mae hwn wrth gwrs yn golygu, pan mae gweinyddion newydd yn cyrraedd, efallai bydd yr hen weinyddion dal yna yn gorffen gwasanaeth y cwsmeriaid gwreiddiol. Mae hwn yn arwain at amser byr lle mae yna mwy o weinyddion ar ddyletswydd nag oedd wedi'i amserlennu.

Er mwyn gweithredu amserlennu rhagdarfiedig neu anrhagdarfiedig, rhaid rhoi'r amserlen mewn tuple, gyda True neu False fel yr ail derm, yn dynodi tarfiadau rhagdarfiedig neu anrhagdarfiedig. Er enghraifft::

    'fy_amserlen_rhagdarfiedig': ([[40, 2], [100, 3], [120, 1], [180, 2], [220, 4], [250, 0]], True)

Ac::

    'fy_amserlen_anrhagdarfiedig': ([[40, 2], [100, 3], [120, 1], [180, 2], [220, 4], [250, 0]], False)

Mae Ciw yn defnyddio amserlennu anrhagdarfiedig fel yr opsiwn diofyn, felly mae'r cod isod yn awgrymu amserlen anrhagdarfiedig::

    'fy_amserlen_arbennig_01': [[40, 2], [100, 3], [120, 1], [180, 2], [220, 4], [250, 0]]

