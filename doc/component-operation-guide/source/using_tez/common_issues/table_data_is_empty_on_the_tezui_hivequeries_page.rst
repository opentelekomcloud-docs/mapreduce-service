:original_name: mrs_01_2076.html

.. _mrs_01_2076:

Table Data Is Empty on the TezUI HiveQueries Page
=================================================

Question
--------

A user logs in to Manager and switches to the Tez web UI page, but no data for the submitted task is displayed on the **Hive Queries** page.

Answer
------

To display task data on the **Hive Queries** page on the Tez web UI, you need to set the following parameters:

On FusionInsight Manager, choose **Cluster** > **Service** > **Hive** and click the **Configurations** tab and then **All Configurations**. In the navigation pane on the left, choose **HiveServer** > **Customization**. Add the following configuration to **hive-site.xml**:

======================= =======================================
Attribute               Attribute Value
======================= =======================================
hive.exec.pre.hooks     org.apache.hadoop.hive.ql.hooks.ATSHook
hive.exec.post.hooks    org.apache.hadoop.hive.ql.hooks.ATSHook
hive.exec.failure.hooks org.apache.hadoop.hive.ql.hooks.ATSHook
======================= =======================================

.. note::

   Data display on TezUI depends on the TimelineServer instance of Yarn. If the TimelineServer instance is faulty or not started, you need to set **yarn.timeline-service.enabled** to **false** in **yarn-site.xml**. Otherwise, the Hive task fails to be executed.

After you configure the parameters and re-execute the Hive task, data can be displayed on the **Hive Queries** page. However, data of previous tasks cannot be displayed.

|image1|

.. |image1| image:: /_static/images/en-us_image_0000001387925652.png
