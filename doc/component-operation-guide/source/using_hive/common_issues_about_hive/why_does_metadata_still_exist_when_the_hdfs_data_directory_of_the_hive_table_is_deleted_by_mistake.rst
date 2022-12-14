:original_name: mrs_01_2343.html

.. _mrs_01_2343:

Why Does Metadata Still Exist When the HDFS Data Directory of the Hive Table Is Deleted by Mistake?
===================================================================================================

Question
--------

The HDFS data directory of the Hive table is deleted by mistake, but the metadata still exists. As a result, an error is reported during task execution.

Answer
------

This is a exception caused by misoperation. You need to manually delete the metadata of the corresponding table and try again.

Example:

Run the following command to go to the console:

**source ${BIGDATA_HOME}/FusionInsight_BASE\_8.1.0.1/install/FusionInsight-dbservice-2.7.0/.dbservice_profile**

**gsql -p 20051 -U hive -d hivemeta -W HiveUser@**

Run the **delete from tbls where tbl_id='xxx';** command.
