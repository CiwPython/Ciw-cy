.. _baulking-functions:

======
Balcio
======

Mae Ciw yn galluogi cwsmeriaid i balcio (osgoi ymuno a'r ciw) wrth gyrraedd y system, yn ôl ffwythiant balcio. Mae'r ffwythiant yn cymryd paramedr :code:`n`, y nifer o gwsmeriaid yn y nod, ac yn dychwelyd tebygolrwydd o falcio.

Er enghraifft, os oes system M/M/1 lle mae cwsmeriaid byth yn balcio os oes llai na 3 cwsmer yn y system, yn balcio gyda thebygolrwydd 0.5 os oes rhwng 3 a 6 cwsmer yn y system, ac yn bacio pob tro os oes mwy na 6 cwsmer yn y system. Fe allwn ddiffinio'r ffwythiant balcio::

    def fy_ffwythiant_balcio(n):
        if n < 3:
           return 0.0
        if n < 7:
           return 0.5
        return 1.0

Yn y geiriadur paramedrau rydym yn dweud wrth Ciw pa nod a dosbarth cwsmer mae'r ffwythiant yma yn berthnasol i, gyda'r allwedd :code:`Baulking_functions`::

    'Baulking_functions': {'Class 0': [fy_ffwythiant_balcio]}

neu os oes ond un dosbarth cwsmer::

    'Baulking_functions': [fy_ffwythiant_balcio]

Nodwch fod balcio yn gweithio ac yn ymddwyn yn wahanol i setio cynhwysedd ciwio. Mae llenwi cynhwysedd ciwio nod yn arwain at gwsmeriaid sy'n cyrraedd yn cael ei *wrthod* (ac yn cael ei recordio yn y :code:`rejection_dict`), ac mae cwsmeriaid sydd yn dod o nodau eraill yn cael eu blocio. Ar y llaw arall nid yw balcio yn effeithio ar y cwsmeriaid sy'n trosglwyddo o nod arall, ac mae'r cwsmeriaid sy'n balcio yn cael ei recordio yn y :code:`baulked_dict`. Mae hwn yn golygu os oes trothwy balcio penderfynedig o 5, ac nad oes cynhwysedd ciwio, yna gall y nifer o gwsmeriaid yn y nod fod yn fwy na 5, oherwydd mae cwsmeriaid sy'n dod o nodau arall yn anwybyddu'r trothwy balcio.

Mae'r :code:`baulked_dict` yn briodwedd o'r gwrthrych Simulation::

    >>> Q.baulked_dict # doctest:+SKIP