.. _ciw-mechanisms:

=============================
Nodiadau ar Mecanweithiau Ciw
=============================

Cyffredinol
~~~~~~~~~~~

Mae Ciw yn defnyddio dull *amserlenni digwiddiadau* (event scheduling) [SW14]_ , sy'n tebyg i'r dull tri cam.
Yn y dull amserlenni digwyddiadau mae yna tri fath o digwyddiad: mae **Digwyddiadau-A** yn symud y cloc ymlaen, **Digwyddiadau-B** yw'r digwyddiadau a drefnwyd o flaen llaw, a **Digwyddiadau-C** yw'r digwyddiadau sy'n cael ei achosi oherwydd fod **Digwyddiadau-B** wedi digwydd.

Fan hyn mae **Digwyddiadau-A** yn cyfateb a symud y cloc ymlaen i'r **Digwyddiad-B** nesaf.
Mae **Digwyddiadau-B** yn cyfateb a naill ai dyfodiad allanol, cwsmer yn gorffen gwasanaeth, neu newid sifft gweinydd.
Mae **Digwyddiadau-C** yn cyfateb a cwsmer yn dechrau gwasanaeth, rhyddhau cwsmer o nod, a cwsmer yn cael ei flocio neu dadflocio.

Yn y dull amserlenni digwyddiadau, mae'r process canlynol yn digwydd:

1. Ymgychwyn yr efelychiad
2. **Cynfnod A**: symud y cloc ymlaen i'r digwyddiad nesaf
3. Cymerwch **Digwyddiad-B** sydd wedi'i trefnu ar gyfer nawr, cario allan y digwyddiad hwnnw
4. Cario allan holl **Digwyddiadau-C** a wnaeth cael eu achosi achos y digwyddiad yn (3.)
5. Ailadroddwch (3.) - (4.) nes bod pob **Digwyddiad-B** sydd wedi'i trefnu ar gyfer nawr wedi'r cario allan
6. Ailadroddwch (2.) - (5.) nes bodloni'r y meini prawf gorffen


Mecanwaith Blocio
~~~~~~~~~~~~~~~~~

Yn Ciw, gweithredir blocio o Fath I (blocio ar ôl gwasanaeth) ar gyfer rhwydweithiau cyfyngedig.

Ar ôl gwasanaeth mae cyrchfan nesaf y cwsmer wedi'i samplu o'r matrics trosglwyddo.
Os oes lle yn y nod cyrchfan, bydd y cwsmer yn ymuno a'r nod yna ac yn dechrau ciwio yna.
Fel arall os yw cynhwysydd ciwio'r nod cyrchfan yn llawn, yna bydd y cwsmer yn cael ei flocio.
Mae'r cwsmer yn aros yn ei nod, gyda'r gweinydd, nes bod bod lle ar gael yn y cyrchfan.
Golygir hwn fod y gweinydd a oedd yn gweinu'r cwsmer yna yn aros yn sownd i'r cwsmer, a ni all y gweinydd yna gweinu unrhyw cwsmer arall neu fod y cwsmer yna yn cael ei dadflocio.

Ar amser y flocio ychwanegwyd gwybodaeth am y blocio i :code:`blocked_queue` y nod cyrchfan, ciw rhithwir sy'n cynnwys gwybodaeth am y cwsmeriaid sydd wedi blocio i'r nod yna, yn ogystal a'r *trefn a flociwyd hwy*
Felly mae'r dilyniant dadflocio yn digwydd yn trefn a flociwyd y cwsmeriaid.

Fe all blocio cylchol arwain at :ref:`llwyrglo <detect-deadlock>`.



Digwyddiadau Cydamserol
~~~~~~~~~~~~~~~~~~~~~~~

Mewn efelychu digwyddiadau arwahanol, mae digwyddiadau cydamserol yn anochel.
Hynny yw dau neu fwy o digwyddiadau wedi'i trefnu i ddigwydd ar yr un pryd.
Fodd bynnag, oherwydd natur efelychiadau digwyddiadau arwahanol, ni all cario allan y digwyddiadau hwn ar yr un pryd, a gall trefn a cariwyd allan y digwyddiadau yma effeithio'u canlyniadau yn fawr.
Er enghraifft, os yw dau cwsmer yn cyrraedd system :ref:`M/M/1 <kendall-notation>` gwag ar yr un pryd: pa cwsmer ddylai dechrau gwasanaeth yn syth a pa cwsmer dylai aros?

I atal unrhyw bias yn Ciw, pryd bynnag mae mwy nag un digwyddiad wedi'i trefnu i digwydd yn cydamserol, dewisir y digwyddiad nesaf ar hap yn unffyrf o'r rhestr digwyddiadau.
