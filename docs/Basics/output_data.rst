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


    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-------------+-----------------------+-------------------------+
    | I.D number | Class | Node | Arrival Date | Waiting Time | Service Start Date | Service Time | Service End Date | Time Blocked | Exit Date | Destination | Queue Size at Arrival | Queue Size at Departure |
    +============+=======+======+==============+==============+====================+==============+==================+==============+===========+=============+=======================+=========================+
    | 227592     | 1     | 1    | 245.601      | 0.0          | 245.601            | 0.563        | 246.164          | 0.0          | 246.164   | -1          | 0                     | 2                       |
    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-------------+-----------------------+-------------------------+
    | 411239     | 0     | 1    | 245.633      | 0.531        | 246.164            | 0.608        | 246.772          | 0.0          | 246.772   | -1          | 1                     | 5                       |
    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-------------+-----------------------+-------------------------+
    | 001195     | 0     | 2    | 247.821      | 0.0          | 247.841            | 1.310        | 249.151          | 0.882        | 250.033   | 1           | 0                     | 0                       |
    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-------------+-----------------------+-------------------------+
    | ...        | ...   | ...  | ...          | ...          | ...                | ...          | ...              | ...          | ...       | ...         | ...                   | ...                     |
    +------------+-------+------+--------------+--------------+--------------------+--------------+------------------+--------------+-----------+-------------+-----------------------+-------------------------+

Mae'r method :code:`write_records_to_file` yn ysgrifennu penawdau fel rhagosodiad. I analluogi'r nodwedd hwn, mewnbwniwch :code:`headers=False`::

    >>> Q.write_records_to_file(<path_i_ffeil>, header=False) # doctest:+SKIP

Gall cael mynediad i'r Records yn Python yn defnyddio'r method :code:`Q.get_all_records()`. Mae hwn yn allbynnu rhestr of tuplau gyda'r enwau canlynol:

    - :code:`id_number`
    - :code:`customer_class`
    - :code:`node`
    - :code:`arrival_date`
    - :code:`waiting_time`
    - :code:`service_start_date`
    - :code:`service_time`
    - :code:`service_end_date`
    - :code:`time_blocked`
    - :code:`exit_date`
    - :code:`destination`
    - :code:`queue_size_at_arrival`
    - :code:`queue_size_at_departure`

Fel enghraifft, gall cael mynediad i'r amser aros y 10fed record fel y ganlyn (Noder fod trefn y records yn ddiystyr)::

    >>> recs = Q.get_all_records # doctest:+SKIP
    >>> recs[10].waiting_time # doctest:+SKIP
    0.0

------------------------
Y Geiriadur Gwrthodiadau
------------------------

Pan mae gan nodau cynhwysedd ciwio cyfyngedig, mae rhai cwsmeriaid yn cael ei wrthod o'r system. Cadwyd data'r cwsmeriaid a wrthodwyd mewn geiriadur :code:`rejection_dict`. Mae hwn yn eiriadur o eiriaduron, gyda nodau a dosbarthau cwsmer fel allweddau, a rhestr o ddyddiadau dyfodiad fel gwerthoedd. Er enghraifft mae :code:`Q.rejection_dict[1][2]` yn rhoi rhestr o'r dyddiadau a wnaeth cwsmeriaid newydd dosbarth 2 cael eu gwrthod o nod 1.