.. _glossary:

Geirfa
======

.. glossary::

   agored
      Disgrifiwyd rhwydwaith ciwio yn agored os yw cwsmeriaid yn gallu cyrraedd o'r tu allan a gadael y system yn gyfan gwbl. (**open**)

   amser cynhesu
      Cyfnod o amser ar ddechrau'r efelychiad lle mar recordiau data ddim yn cyfri tuag at unrhyw dadansoddi. Mae hwn oherwydd bod y rhagfarn o ddechrau'r efelychiad o system wag. Mae canlyniadau ond yn cael eu dadansoddi ar ôl i'r system cyrraedd rhyw fath o gyflwr-cyson. (**warm-up time**)

   amserlen gwaith
      Amserlen yn dynodi faint o weinyddion sy'n gweithio yng nghyfnodau amser penodol ar gyfer nod penodol. Mae amserlenni gwaith yn gylchol, ac felly unwaith cyrhaeddir y `cyfnod y cylchred` mae'r amserlen yn dechrau eto. (**work schedule**)

   amserlen gweinyddion
      Ymgyfnewidiol gyda `amserlen gwaith`. (**server schedule**)

   blocio
      Mae blocio yn digwydd pan mae cwsmer yn gorffen gwasanaeth ac yn trio trosglwyddo i'w nod gyrchfan, ond mae cynhwysedd ciwio'r nod yna yn llawn. Yn yr achos hwn mae blocio yn digwydd lle mae'r cwsmer yn aros yn y nod gwreiddiol, yn dal i gynnal gweinydd, nes bod lle yn dod yn rhydd yn y nod gyrchfan. Yn ystod yr amser blocio yma, nid yw'r gweinydd yn rhydd i weini unrhyw mwy o gwsmeriaid. (**blocking**)

   caeedig
      Disgrifiwyd rhwydwaith ciwio yn gaeedig os nad yw cwsmeriaid yn gallu cyrraedd o'r tu allan neu adael y system yn gyfan gwbl. (**closed**)

   canolfan gwasanaeth
      Rhan o'r nod lle mae cwsmeriaid yn cael eu gweini. Gall hwn cynnwys gweinyddwyr paralel lluosog. (Ymgyfnewidiol gyda `gorsaf gwasanaeth`). (**service centre**)

   ciw
      Rhan o'r nod lle mae cwsmeriaid yn aros. Mae'r aros yn dilyn disgyblaeth cyntaf-i-mewn-cyntaf 
      -allan (FIFO). (**queue**)

   cwsmer
      Yr endidau sy'n cael eu hefelychu wrth iddynt aros, treulio amser yn wasanaeth, a llifo trwy'r system. (Ymgyfnewidiol gyda 'unigolyn'.) (**customer**)

   cyfnod y cylchred
      Ystod cylchred yr `amserlen gwaith`. (**cycle length**)

   cyfyngedig
      Disgrifiwyd rhwydwaith ciwio yn gyfyngedig os oes yna nodau gyda chynhwysedd ciwio cyfyngedig, ac mae blocio yn digwydd. (**restricted**)

   cynhwysedd ciwio
      Cynhwysedd ciwio nod yw'r nifer macsimwm o gwsmeriaid a chaniateir i aros wrth y nod ar unrhyw amser. (**queueing capacity**)

   dosraniad dyfodiadau
      Y dosraniad a deilliwyd amseroedd rhwng-dyfodiad nod. (**arrival distribution**)

   dosraniad gwasanaeth
      Y dosraniad a deilliwyd amseroedd gwasanaeth nod. (**service distribution**)

   dwysedd traffig
      Mesur o pa mor brysur yw'r system yw'r dwysedd traffig. Ar gyfer nod penodol diffiniwyd dwysedd traffig fel cymhareb amseroedd gwasanaeth cymedrig a'r amseroedd rhwng-dyfodiad cymedrig. (**traffic intensity**)

   dyfodiad
      Y digwyddiad lle mae cwsmer yn mynychu nod. (**arrival**)

   dyfodiad allanol
      Dyfodiad allanol yw dyfodiad o du allan y rhwydwaith. Hynny yw pob dyfodiad i nodau lle ni ddaeth y cwsmer o nod arall. (**external arrival**)

   gorsaf gwasanaeth
      Ymgyfnewidiol gyda `canolfan gwasanaeth`. (**service station**)

   gwasanaeth
      Y cyfnod lle mae cwsmer yn treulio amser gyda gweinydd. Dyma'r gweithgaredd y mae cwsmeriaid yn aros i ddechrau. (**service**)

   gweinydd
      Adnodd y mae cwsmer yn cynnal ar gyfer yr ystod y gwasanaeth. Mae'r gweinydd hefyd yn cael ei chynnal tra bod y cwsmer wedi'i flocio. (**server**)

   llwyrglo
      Cyflwr o flocio cilyddol lle all is-set o gwsmeriaid byth symud oherwydd blocio cylchol. (**deadlock**)

   matrics trosglwyddiadau
      Matrics o debygolrwyddau trosglwyddo. Mae'r cofnod yn rhes `i` o golofn `j`, :math:`r_{ij}`, yw'r tebygolrwydd o drosglwyddo i nod `j` ar ôl gorffen gwasanaeth yn nod `i`. (**transition matrix**)

   nod
      Mae nod yn cynnwys ciw o gwsmeriaid sy'n aros, a gorsaf gwasanaeth o weinyddion. (**node**)

   rhwydwaith ciwio
      Set o nodau, wedi'i chysylltu mewn rhwydwaith gan fatrics trosglwyddiadau. (**queueing network**)

   unigolyn
      Ymgyfnewidiol gyda `cwsmer`. (**individual**)