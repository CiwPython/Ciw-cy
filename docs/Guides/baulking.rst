.. _baulking-functions:

=====================================
Sut i Efelychu Cwsmeriaid Sy'n Balcio
=====================================

Mae Ciw yn gadael i gwsmeriaid balcio (dewis peidio ymuno a chiw) pan maent yn dyfodi, yn ôl ffwythiannau balcio.
Mae'r ffwythiannau yma yn cymryd paramedr :code:`n`, nifer o unigolion wrth y nod, ac yn rhoi tebygolrwydd o'r cwsmer balcio.

Er enghraifft, mae ganddynt hwy system :ref:`M/M/1 <kendall-notation>` lle mae cwsmeriaid:

+ Byth yn balcio os oes llai na 3 cwsmer yn y system
+ Yn cael tebygolrwydd 0.5 o balcio os oes rhwng 3 a 6 cwsmer yn y system
+ Trwy'r amser yn balcio os oes mwy na 6 cwsmer yn y system

Fe allwn ddiffinio'r ffwythiant balcio canlynol::

    >>> def probability_of_baulking(n):
    ...     if n < 3:
    ...         return 0.0
    ...     if n < 7:
    ...         return 0.5
    ...     return 1.0

Wrth greu'r gwrthrych Network, rydym yn dweud wrth Ciw pa nod a dosbarth cwsmer mae'r ffwythiant yma yn berthnasol ar gyfer, gyda'r allweddair :code:`Baulking_functions`::
	
	>>> import ciw
	>>> N = ciw.create_network(
	...      Arrival_distributions={'Class 0': [['Exponential', 5]]},
	...      Service_distributions={'Class 0': [['Exponential', 10]]},
	...      Baulking_functions={'Class 0': [probability_of_baulking]},
	...      Number_of_servers=[1]
	... )

Pan mae'r system wedi gorffen efelychu, cofnodwyd y cwsmeriaid a wnaeth balcio yn :code:`baulked_dict` y gwrthrych Simulation.
Geiriadur yw hwn sy'n mapio rhifau nod i eiriaduron.
Mae'r geiriaduron yma yn mapio rhifau dosbarthau cwsmer i restr o ddyddiadau lle wnaeth cwsmer balcio::

	>>> ciw.seed(1)
	>>> Q = ciw.Simulation(N)
	>>> Q.simulate_until_max_time(45.0)
	>>> Q.baulked_dict
	{1: {0: [21.1040..., 42.2023..., 43.7558..., 43.7837..., 44.2266...]}}

Nodwch fod balcio yn gweithio ac yn ymddwyn yn wahanol i setio cynhwysedd ciwio.
Mae llenwi cynhwysedd ciwio nod yn arwain at dyfodiadau newydd yn cael eu *wrthod** (a chofnodwyd y rhain yn y :code:`rejection_dict`), a chwsmeriaid sy'n trosglwyddo o nod arall yn cael eu blocio.
Ar y llaw arall nid yw balcio yn effeithio cwsmeriaid sy'n trosglwyddo o nod arall, a chofnodwyd cwsmeriaid a wnaeth balcio yn y :code:`baulked_dict`.
Mae hwn yn golygu os osodwyd trothwy balcio penderfynedig o 5, ond ni osodwyd cynhwysedd ciwio, yna gall nifer o unigolion wrth y nod yna bod yn fwy na 5, oherwydd bod cwsmeriaid sy'n trosglwyddo o nodau arall yn anwybyddu'r trothwy balcio.