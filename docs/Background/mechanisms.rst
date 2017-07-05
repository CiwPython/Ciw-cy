.. _ciw-mechanisms:

=============================
Nodiadau ar Fecanweithiau Ciw
=============================

Cyffredinol
~~~~~~~~~~~

Mae Ciw yn defnyddio dull *amserlenni digwyddiadau* (event scheduling) [SW14]_ , sy'n debyg i'r dull tri cham.
Yn y dull amserlenni digwyddiadau mae yna tri math o ddigwyddiad: mae **Digwyddiadau-A** yn symud y cloc ymlaen, **Digwyddiadau-B** yw'r digwyddiadau a drefnwyd o flaen llaw, a **Digwyddiadau-C** yw'r digwyddiadau sy'n cael ei achosi oherwydd bod **Digwyddiadau-B** wedi digwydd.

Fan hyn mae **Digwyddiadau-A** yn cyfateb a symud y cloc ymlaen i'r **Digwyddiad-B** nesaf.
Mae **Digwyddiadau-B** yn cyfateb a naill ai dyfodiad allanol, cwsmer yn gorffen gwasanaeth, neu newid sifft gweinydd.
Mae **Digwyddiadau-C** yn cyfateb a chwsmer yn dechrau gwasanaeth, rhyddhau cwsmer o nod, a chwsmer yn cael ei flocio neu ddadflocio.

Yn y dull amserlenni digwyddiadau, mae'r proses canlynol yn digwydd:

1. Ymgychwyn yr efelychiad
2. **Cyfnod A**: symud y cloc ymlaen i'r digwyddiad nesaf
3. Cymerwch **Digwyddiad-B** sydd wedi'i threfnu ar gyfer nawr, cario allan y digwyddiad hwnnw
4. Cario allan holl **Digwyddiadau-C** a wnaeth cael eu hachosi achos y digwyddiad yn (3.)
5. Ailadroddwch (3.) - (4.) nes bod pob **Digwyddiad-B** sydd wedi'i threfnu ar gyfer nawr wedi'r cario allan
6. Ailadroddwch (2.) - (5.) nes bodloni'r meini prawf gorffen


Mecanwaith Blocio
~~~~~~~~~~~~~~~~~

Yn Ciw, gweithredir blocio o Fath I (blocio ar ôl gwasanaeth) ar gyfer rhwydweithiau cyfyngedig.

Ar ôl gwasanaeth mae cyrchfan nesaf y cwsmer wedi'i samplu o'r matrics trosglwyddo.
Os oes lle yn y nod cyrchfan, bydd y cwsmer yn ymuno a'r nod yna ac yn dechrau ciwio yna.
Fel arall os yw cynhwysydd ciwio'r nod cyrchfan yn llawn, yna bydd y cwsmer yn cael ei flocio.
Mae'r cwsmer yn aros yn ei nod, gyda'r gweinydd, nes bod lle ar gael yn y cyrchfan.
Golygir hwn fod y gweinydd a oedd yn gweini’r cwsmer yna yn aros yn sownd i'r cwsmer, a ni all y gweinydd yna gweini unrhyw gwsmer arall neu fod y cwsmer yna yn cael ei dadflocio.

Ar amser y flocio ychwanegwyd gwybodaeth am y blocio i :code:`blocked_queue` y nod cyrchfan, ciw rhithwir sy'n cynnwys gwybodaeth am y cwsmeriaid sydd wedi blocio i'r nod yna, yn ogystal â'r *trefn a flociwyd hwy*
Felly mae'r dilyniant dadflocio yn digwydd yn drefn a flociwyd y cwsmeriaid.

Fe all blocio cylchol arwain at :ref:`llwyrglo <detect-deadlock>`.


.. _simultaneous_events:

Digwyddiadau Cydamserol
~~~~~~~~~~~~~~~~~~~~~~~

Mewn efelychu digwyddiadau arwahanol, mae digwyddiadau cydamserol yn anochel.
Hynny yw dau neu fwy o ddigwyddiadau wedi'i threfnu i ddigwydd ar yr un pryd.
Fodd bynnag, oherwydd natur efelychiadau digwyddiadau arwahanol, ni all cario allan y digwyddiadau hyn ar yr un pryd, a gall trefn a chariwyd allan y digwyddiadau yma effeithio'u canlyniadau yn fawr.
Er enghraifft, os yw dau gwsmer yn cyrraedd system :ref:`M/M/1 <kendall-notation>` gwag ar yr un pryd: pa gwsmer ddylai dechrau gwasanaeth yn syth a pa gwsmer dylai aros?

I atal unrhyw fias yn Ciw, pryd bynnag mae mwy nag un digwyddiad wedi'i threfnu i ddigwydd yn gydamserol, dewisir y digwyddiad nesaf ar hap yn unffurf o'r rhestr digwyddiadau.
