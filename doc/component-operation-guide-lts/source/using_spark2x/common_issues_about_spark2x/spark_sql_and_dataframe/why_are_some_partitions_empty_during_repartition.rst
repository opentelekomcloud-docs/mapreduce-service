:original_name: mrs_01_2030.html

.. _mrs_01_2030:

Why Are Some Partitions Empty During Repartition?
=================================================

Question
--------

During the repartition operation, the number of blocks (**spark.sql.shuffle.partitions**) is set to 4,500, and the number of keys used by repartition exceeds 4,000. It is expected that data corresponding to different keys can be allocated to different partitions. However, only 2,000 partitions have data, and data corresponding to different keys is allocated to the same partition.

Answer
------

This is normal.

The partition to which data is distributed is obtained by performing a modulo operation on hashcode of a key. Different hashcodes may have the same modulo result. In this case, data is distributed to the same partition, as a result, some partitions do not have data, and some partitions have data corresponding to multiple keys.

You can adjust the value of **spark.sql.shuffle.partitions** to adjust the cardinality during modulo operation and improve the unevenness of data blocks. After multiple verifications, it is found that the effect is good when the parameter is set to a prime number or an odd number.

Configure the following parameters in the **spark-defaults.conf** file on the Driver client.

.. table:: **Table 1** Parameter Description

   +------------------------------+-------------------------------------------------------------+---------------+
   | Parameter                    | Description                                                 | Default Value |
   +==============================+=============================================================+===============+
   | spark.sql.shuffle.partitions | Number of shuffle data blocks during the shuffle operation. | 200           |
   +------------------------------+-------------------------------------------------------------+---------------+
