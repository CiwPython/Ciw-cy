.. _output-file:

=============
Y Data Allbwn
=============

Unwaith fod efelychiad wedi rhedeg, fe allwch alw'r method canlynol i ysgrifennu ffeil ddata::

    >>> Q.write_records_to_file(<path_i_ffeil>) # doctest:+SKIP

Nid yw'r ffeil yn cynnwys ystadegau cryno, ond mae'n cynnwys yr holl wybodaeth a ddigwyddodd yn ystod yr efelychiad yn fformat crai.
Pob tro mae unigolyn yn cyflawni gwasanaeth yn orsaf gwasanaeth, mae record data o'r gwasanaeth hwnna yn cael ei chadw.
Mae'r ffeil yma yn cynnwys yr holl recordiau data o holl wasanaethau holl gwsmeriaid ym mhob nod yn ystod amser yr efelychiad.

Mae'r tabl canlynol yn crynhoi'r colofnau:


    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-----------------------+-------------------------+
    | I.D number | Class | Node | Arrival Date | Waiting Time | Service Start Date | Service Time | Service End Date | Time Blocked | Exit Date | Queue Size at Arrival | Queue Size at Departure |
    +============+=======+======+==============+==============+====================+==============+==================+==============+===========+=======================+=========================+
    | 227592     | 1     | 1    | 245.601      | 0.0          | 245.601            | 0.563        | 246.164          | 0.0          | 246.164   | 0                     | 2                       |
    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-----------------------+-------------------------+
    | 411239     | 0     | 1    | 245.633      | 0.531        | 246.164            | 0.608        | 246.772          | 0.0          | 246.772   | 1                     | 5                       |
    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-----------------------+-------------------------+
    | 001195     | 0     | 2    | 247.821      | 0.0          | 247.841            | 1.310        | 249.151          | 0.882        | 250.033   | 0                     | 0                       |
    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-----------------------+-------------------------+
    | ...        | ...   | ...  | ...          | ...          | ...                | ...          | ...              | ...          | ...       | ...                   |                         |
    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-----------------------+-------------------------+

Mae'r method :code:`write_records_to_file` yn ysgrifennu penawdau fel rhagosodiad. I analluogi'r nodwedd hwn, mewnbwniwch :code:`headers=False`::

    >>> Q.write_records_to_file(<path_i_ffeil>, header=False) # doctest:+SKIP
