.. _refs-results:

==================
Rhestr Canlyniadau
==================

Pob tro mae unigolyn yn cwblhau gwasanaeth wrth orsaf wasanaeth, cadwyd cofnod data o'r gwasanaeth hwnna.
Dylai'r cofnodion yma edrych yn debyg i'r tabl isod:

    +--------+-------+------+--------------+-----------+--------------------+--------------+------------------+--------------+-----------+-------+-----------------------+-----------------------+
    | I.D    | Class | Node | Arrival Date | Wait Time | Service Start Date | Service Time | Service End Date | Time Blocked | Exit Date | Dest. | Queue Size at Arrival | Queue Size at Depart. |
    +========+=======+======+==============+===========+====================+==============+==================+==============+===========+=======+=======================+=======================+
    | 22759  | 1     | 1    | 245.601      | 0.0       | 245.601            | 0.563        | 246.164          | 0.0          | 246.164   | -1    | 0                     | 2                     |
    +--------+-------+------+--------------+-----------+--------------------+--------------+------------------+--------------+-----------+-------+-----------------------+-----------------------+
    | 41129  | 0     | 1    | 245.633      | 0.531     | 246.164            | 0.608        | 246.772          | 0.0          | 246.772   | -1    | 1                     | 5                     |
    +--------+-------+------+--------------+-----------+--------------------+--------------+------------------+--------------+-----------+-------+-----------------------+-----------------------+
    | 00195  | 0     | 2    | 247.821      | 0.0       | 247.841            | 1.310        | 249.151          | 0.882        | 250.033   | 1     | 0                     | 0                     |
    +--------+-------+------+--------------+-----------+--------------------+--------------+------------------+--------------+-----------+-------+-----------------------+-----------------------+
    | ...    | ...   | ...  | ...          | ...       | ...                | ...          | ...              | ...          | ...       | ...   | ...                   | ...                   |
    +--------+-------+------+--------------+-----------+--------------------+--------------+------------------+--------------+-----------+-------+-----------------------+-----------------------+

Fe allwch gael mynediad i'r cofnodion yma fel rhestr o tuples enwedig, yn defnyddio dull :code:`get_all_records` y gwrthrych Simulation.

    >>> recs = Q.get_all_records() # doctest:+SKIP

Tuples enwedig yw'r cofnodion data sydd wedi cynnwys yn y rhestr yma, gyda'r enwau newidynnau canlynol:

    - :code:`id_number`
       - Rhif adnabod unigryw'r cwsmer yna.
    - :code:`customer_class`
       - Rhif dosbarth cwsmer y cwsmer yna. Os defnyddir dosbarthau cwsmer deinamig, hwn yw dosbarth cwsmer blaenorol y cwsmer, cyn samplwyd dosbarth cwsmer newydd.
    - :code:`node`
       - Rhif y nod lle digwyddodd y gwasanaeth.
    - :code:`arrival_date`
       - Y dyddiad a wnaeth y cwsmer cyrraedd y nod, y dyddiad gwnaeth y cwsmer ymuno a'r ciw.
    - :code:`waiting_time`
       - Faint o amser arhosodd y cwsmer am wasanaeth wrth y nod yma.
    - :code:`service_start_date`
       - Y dyddiad a ddechreuodd gwasanaeth wrth y nod yna.
    - :code:`service_time`
       - Faint o amser gwariodd y cwsmer yn wasanaeth wrth y nod yna.
    - :code:`service_end_date`
       - Y dyddiad gorffennodd y gwasanaeth wrth y nod yna.
    - :code:`time_blocked`
       - Faint o amser gwariodd y cwsmer wedi'i flocio wrth y nod yna. Hynny yw r amser rhwng gorffen gwasanaeth a gadael y nod.
    - :code:`exit_date`
       - Y dyddiad gadawodd y cwsmer y nod. Gall hyn fod yn syth ar ôl i wasanaeth gorffen os nad oedd blocio, neu ar ôl rhyw gyfnod o flocio.
    - :code:`destination`
       - Rhif cyrchfan y cwsmer, hynny yw y nod nesaf fyd y cwsmer yn ymuno ar ôl gadael y nod presennol. Os yw'r cwsmer yn gadael y system, -1 fydd hwn.
    - :code:`queue_size_at_arrival`
       - Hyd y ciw ar ddyddiad dyfodi'r cwsmer. Nid yw'n cynnwys yr unigolyn ei hun.
    - :code:`queue_size_at_departure`
       - Hyd y ciw ar ddyddiad gadael y cwsmer. Nid yw'n cynnwys yr unigolyn ei hun.
