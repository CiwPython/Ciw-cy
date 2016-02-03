.. _custom-distributions:

=================================================
Creu FfDT Arwahanol ar Gyfer Amseroedd Gwasanaeth
=================================================

Mae Ciw yn galluogi defnyddwyr i ddiffinio ffwythiannau dwysedd tebygolrwydd arwahanol eu hun ar gyfer amseroedd gwasanaeth.
Gall esiampl o ddosraniad arwahanol edrych fel hyn:

	+------+------+------+------+------+------+------+
	| P(X) |  0.1 |  0.1 |  0.3 |  0.2 |  0.2 |  0.1 |
	+------+------+------+------+------+------+------+
	|   X  |  9.5 | 10.2 | 10.6 | 10.9 | 11.7 | 12.1 | 
	+------+------+------+------+------+------+------+

Er mwyn diffinio'r FfDT hwn, rhaid rhoi enw iddo.
Gadewch i ni alw'r dosraniad yma :code:`fy_nosraniad_arbennig_01`.

I weithredu hwn yn y geiriadur paramedrau, angen datgan y dosraniad gwasanaeth ar gyfer y dosbarth cwsmer a'r nod yna fel :code:`Custom`, a rhoi enw'r dosraniad fel paramedr::


    'Service_distributions':{'Class 0':[['Custom', 'fy_nosraniad_arbennig_01'], ['Exponential', 0.1]], 'Class 1':[['Exponential', 0.3], ['Exponential', 0.1]]}

Yn y ffeil :code:`parameters.yml`, o dan :code:`Serivce_rates`, ar gyfer y dosbarth cwsmer a nod priodol rhowch :code:`Custom` ac enw'r dosraniad oddi tanno.
Dangosir esiampl::

    Service_distributions:
      Class 0:
      - - Custom
        - fy_nosraniad_arbennig_01
      - - Exponential
        - 0.1
      Class 1:
      - - Exponential
        - 0.3
      - - Exponential
        - 0.1

Mae hwn yn dweud wrth Ciw bydd pob cwsmer Class 0 yn Nod 1 yn cael amser gwasanaeth a dynnwyd o'r dosraniad :code:`fy_nosraniad_arbennig_01`.
Nid yw'r dosraniad hwn wedi'i ddiffinio eto.

I ddiffinio'r dosraniad, ychwanegwch y canlynol i'r geiriadur paramedrau::

    'my_special_distribution':[[0.1, 9.5], [0.1, 10.2], [0.3, 10.6], [0.2, 10.9], [0.2, 11.7], [0.2, 12.1]]

I ddiffinio'r dosraniad yn y ffeil :code:`parameters.yml`, ychwanegwch y llinellau canlynol i'r diwedd::

    fy_nosraniad_arbennig_01:
      - - 0.1
        - 9.5
      - - 0.1
        - 10.2
      - - 0.3
        - 10.6
      - - 0.2
        - 10.9
      - - 0.2
        - 11.7
      - - 0.1
        - 12.1

Fan hyn rydym yn dweud samplwyd y gwerth 9.5 gyda thebygolrwydd 0.1, samplwyd y gwerth 10.2 gyda thebygolrwydd 0.1, ayyb.
Mae hwn yn diffinio'r FfDT arwahanol yn llawn.

Noder:

- Ar gyfer pob dosraniad, rhaid i'r tebygolrwydd symio i 1.
- Fe allwch ychwanegu cynifer o ddosraniadau tebygolrwydd arfer ag y dymunwch.