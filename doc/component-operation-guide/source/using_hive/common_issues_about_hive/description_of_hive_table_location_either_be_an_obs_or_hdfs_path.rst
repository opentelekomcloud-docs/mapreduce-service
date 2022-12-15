:original_name: mrs_01_1763.html

.. _mrs_01_1763:

Description of Hive Table Location (Either Be an OBS or HDFS Path)
==================================================================

Question
--------

Can Hive tables be stored in OBS or HDFS?

Answer
------

#. The location of a common Hive table stored on OBS can be set to an HDFS path.
#. In the same Hive service, you can create tables stored in OBS and HDFS, respectively.
#. For a Hive partitioned table stored on OBS, the location of the partition cannot be set to an HDFS path. (For a partitioned table stored on HDFS, the location of the partition cannot be changed to OBS.)
