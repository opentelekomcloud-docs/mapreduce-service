:original_name: mrs_01_2076.html

.. _mrs_01_2076:

Table Data Is Empty on the TezUI HiveQueries Page
=================================================

Question
--------

A user logs in to Manager and switches to the Tez web UI page, but no data for the submitted task is displayed on the **Hive Queries** page.

Answer
------

To display Hive Queries task data on the Tez web UI, you need to set the following parameters:

On FusionInsight Manager, choose **Cluster** > **Services** > **Hive** > **Configurations** > **All Configurations** > **HiveServer** > **Customization**. Add the following configuration to **hive-site.xml**:

======================= =======================================
Attribute               Attribute Value
======================= =======================================
hive.exec.pre.hooks     org.apache.hadoop.hive.ql.hooks.ATSHook
hive.exec.post.hooks    org.apache.hadoop.hive.ql.hooks.ATSHook
hive.exec.failure.hooks org.apache.hadoop.hive.ql.hooks.ATSHook
======================= =======================================

.. note::

   Data display on TezUI depends on the TimelineServer instance of Yarn. If the TimelineServer instance is faulty or not started, you need to set **yarn.timeline-service.enabled** to **false** in **yarn-site.xml**. Otherwise, the Hive task fails to be executed.
