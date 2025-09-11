:original_name: ALM-38017.html

.. _ALM-38017:

ALM-38017 Partition Reassignment Duration Exceeds the Threshold
===============================================================

Alarm Description
-----------------

The system checks the partition reassignment time every 10 minutes. The check interval can be modified by the Kafka configuration **auto.reassign.check.interval.ms**. This alarm is generated when the partition reassignment triggered by a Broker scale-out takes more time than the threshold (1440 minutes by default, which can be modified by the Kafka configuration **reassignment.total.time.threshold**).

This alarm is cleared when the partition workload balancing is complete.

.. note::

   This alarm applies only to MRS 3.5.0 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
38017    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------------+------------------------------------------------------------------+
| Type                   | Parameter         | Description                                                      |
+========================+===================+==================================================================+
| Location Information   | Source            | Specifies the cluster for which the alarm was generated.         |
+------------------------+-------------------+------------------------------------------------------------------+
|                        | ServiceName       | Specifies the cluster service for which the alarm was generated. |
+------------------------+-------------------+------------------------------------------------------------------+
|                        | RoleName          | Specifies the role for which the alarm was generated.            |
+------------------------+-------------------+------------------------------------------------------------------+
|                        | HostName          | Specifies the host for which the alarm was generated.            |
+------------------------+-------------------+------------------------------------------------------------------+
| Additional Information | Trigger Condition | Specifies the alarm triggering condition.                        |
+------------------------+-------------------+------------------------------------------------------------------+

Impact on the System
--------------------

The Kafka service has unbalanced load for a long time, which may deteriorate the read and write performance.

Possible Causes
---------------

The amount of data in a partition to be migrated is too large, and the allowed triffic is low.

Handling Procedure
------------------

#. Log in to the Kafka web UI.

   a. Log in to MRS Manager as a user who has the permission to access the Kafka web UI.
   b. Choose **Cluster** > **Services** > **Kafka**.
   c. On the right of **KafkaManager Web UI**, click the URL to access the Kafka web UI.

#. Click **Current Reassign Status** to view the partition reassignment tasks.

   |image1|

#. Check the status of the partitions that are being migrated. If the progress remains unchanged for a long time, click **Modify Reassignment Throttle** to check whether the value of the **Throttle** parameter is too small.

   |image2|

   -  If yes, adjust the **Throttle** parameter during off-peak hours and click **OK** to accelerate the migration. Run the command in :ref:`4 <alm-38017__en-us_topic_0000001991090838_en-us_topic_0000001960602962_li986485621319>`.
   -  If no, go to :ref:`5 <alm-38017__en-us_topic_0000001991090838_li42224042151734>`.

#. .. _alm-38017__en-us_topic_0000001991090838_en-us_topic_0000001960602962_li986485621319:

   Wait for 10 minutes and check whether the partition migration progress changes significantly.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-38017__en-us_topic_0000001991090838_li42224042151734>`.

**Collect fault information.**

5. .. _alm-38017__en-us_topic_0000001991090838_li42224042151734:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **Kafka** for the target cluster.

7. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000002380470088.png
.. |image2| image:: /_static/images/en-us_image_0000002414069445.png
