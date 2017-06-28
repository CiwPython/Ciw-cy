.. _kendall-notation:

===============
Nodiant Kendall
===============

Defnyddir nodiant Kendall yn i dynodi system ciwio node sengl yn llawfer [WS09]_.

Nodweddwyd ciw gan:

.. math::

    A/B/C/X/Y/Z

lle mae:

+ :math:`A` yn dynodi dosraniad yr amseroedd rhwng-dyfodiad
+ :math:`B` yn dynodi dosraniad yr amseroedd gwasanaeth
+ :math:`C` yn dynodi dosraniad nifer o weinyddion
+ :math:`X` yn dynodi y cynhwysedd ciwio
+ :math:`Y` yn dynodi maint y poblogaeth y cwsmeriaid
+ :math:`Z` yn dynodi y disgybleth ciwio

Ar gyfer y paramedrau :math:`A` a :math:`B` mae yna nifer o nodiannau llwfer ar gael. Er enghraifft:

+ :math:`M`: dosraniad Markovaidd neu Esbonyddol
+ :math:`E`: dosraniad Erlang (achos arbennig o'r dosraniad Gama)
+ :math:`C_k`: dosraniad Coxaidd o drefn :math:`k`
+ :math:`D`: dosraniad Penderfynedig
+ :math:`G` / :math:`GI`: dosraniad Cyffredinol / Cyffredinol annibynnol

MAe'r paramedrau :math:`X`, :math:`Y` a :math:`Z` yn opsiynnol, a cymerwn yn ganiataol eu fod yn :math:`\infty`, :math:`\infty`, a Cyntaf Mewn Cyntaf Allan (FIFO) yn ol eu drefn.
Opsiynnau arall ar gyfer y disgyblaeth ciwio :math:`Z` yw SIRO (Gwasanaeth Mewn Trefn Ar Hap), LIFO (Olaf Mewn Cyntaf Allan), a PS (Rhannu Prosessau).

Rhai enghraifftiau:

+ :math:`M/M/1`:
   + Amseroedd rhwng-dyfodiad Esbonyddol
   + Amseroedd gwasanaeth Esbonyddol
   + 1 gweinydd
   + Cynhwysedd ciwio anfeidraidd
   + Poblogaeth anfeidraidd
   + Cyntaf mewn cyntaf allan

+ :math:`M/D/\infty/\infty/1000`:
   + Amseroedd rhwng-dyfodiad Esbonyddol
   + Amseroedd gwasanaeth Penderfynnol
   + Nifer anfeidraidd o weinyddion
   + Cynhwysedd ciwio anfeidraidd
   + Poblogaeth o 1000 cwsmer
   + Cyntaf mewn cyntaf allan

+ :math:`G/G/1/\infty/\infty/\text{SIRO}`:
   + Amseroedd rhwng-dyfodiad Cyffredinol
   + Amseroedd gwasanaeth Cyffredinol
   + 1 gweinydd
   + Cynhwysedd ciwio anfeidraidd
   + Poblogaeth anfeidraidd
   + Gwasanaeth mewn trefn ar hap

+ :math:`M/M/4/5`:
   + Amseroedd rhwng-dyfodiad Esbonyddol
   + Amseroedd gwasanaeth Esbonyddol
   + 4 gweinydd
   + Cyhwysedd ciwio o 5
   + Poblogaeth anfeidraidd
   + Cyntaf mewn cyntaf allan

