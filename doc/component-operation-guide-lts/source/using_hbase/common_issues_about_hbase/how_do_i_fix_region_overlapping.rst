:original_name: mrs_01_1660.html

.. _mrs_01_1660:

How Do I Fix Region Overlapping?
================================

Question
--------

When the HBaseFsck tool is used to check the region status, if the log contains **ERROR: (regions region1 and region2) There is an overlap in the region chain** or **ERROR: (region region1) Multiple regions have the same startkey: xxx**, overlapping exists in some regions. How do I solve this problem?

Answer
------

To rectify the fault, perform the following steps:

#. .. _mrs_01_1660__en-us_topic_0000001173949842_l57959cf11dc74b388d62a55b172f9fa6:

   Run the **hbase hbck -repair** *tableName* command to restore the table that contains overlapping.

#. Run the **hbase hbck** *tableName* command to check whether overlapping exists in the restored table.

   -  If overlapping does not exist, go to :ref:`3 <mrs_01_1660__en-us_topic_0000001173949842_lc78ee31171b54bc988743bab2a08bbc9>`.
   -  If overlapping exists, go to :ref:`1 <mrs_01_1660__en-us_topic_0000001173949842_l57959cf11dc74b388d62a55b172f9fa6>`.

#. .. _mrs_01_1660__en-us_topic_0000001173949842_lc78ee31171b54bc988743bab2a08bbc9:

   Log in to FusionInsight Manager and choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase** > **More** > **Perform HMaster Switchover** to complete the HMaster active/standby switchover.

#. Run the **hbase hbck** *tableName* command to check whether overlapping exists in the restored table.

   -  If overlapping does not exist, no further action is required.
   -  If overlapping still exists, start from :ref:`1 <mrs_01_1660__en-us_topic_0000001173949842_l57959cf11dc74b388d62a55b172f9fa6>` to perform the recovery again.
