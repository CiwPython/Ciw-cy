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


Diffinir y dosraniad yma gan rhestr o rhestrau::

    [[0.1, 9.5], [0.1, 10.2], [0.3, 10.6], [0.2, 10.9], [0.2, 11.7], [0.2, 12.1]]

Fan hyn rydym yn dweud samplwyd y gwerth 9.5 gyda thebygolrwydd 0.1, samplwyd y gwerth 10.2 gyda thebygolrwydd 0.1, ayyb. Noder rhaid i'r tebygolrwydd symio i 1.

I weithredu hwn yn y geiriadur paramedrau, angen datgan y dosraniad gwasanaeth ar gyfer y dosbarth cwsmer a'r nod yna fel :code:`Custom`, a rhoi enw'r dosraniad fel paramedr::


    'Service_distributions':{'Class 0':[['Custom', 'fy_nosraniad_arbennig_01'], ['Exponential', 0.1]], 'Class 1':[['Exponential', 0.3], ['Exponential', 0.1]]}

Yn y ffeil :code:`parameters.yml`, o dan :code:`Serivce_distributions`, ar gyfer y dosbarth cwsmer a nod priodol rhowch :code:`Custom` ac enw'r dosraniad oddi tanno.
Dangosir esiampl::

    Service_distributions:
      Class 0:
      - - Custom
        - [[0.1, 9.5], [0.1, 10.2], [0.3, 10.6], [0.2, 10.9], [0.2, 11.7], [0.2, 12.1]]
      - - Exponential
        - 0.1
      Class 1:
      - - Exponential
        - 0.3
      - - Exponential
        - 0.1
