:original_name: ALM-50845.html

.. _ALM-50845:

ALM-50845 Spark Task Data Skew
==============================

Alarm Description
-----------------

The system periodically checks skewed Spark data. This alarm is generated when the amount of skewed Spark data exceeds the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50845    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+-------------+--------------------------------------------------------------------+
| Parameter   | Description                                                        |
+=============+====================================================================+
| Source      | Specifies the cluster or system for which the alarm was generated. |
+-------------+--------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm was generated.           |
+-------------+--------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm was generated.              |
+-------------+--------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm was generated.              |
+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

If Spark data on the node has severely skewed, the service efficiency of the server decreases.

Possible Causes
---------------

The load tilt is too large, and the load pressure is too high.

Handling Procedure
------------------

**Change the Spark parameter value to the native setting.**

#. Log in to the Spark client node, go to the **/opt/client/Spark/spark/conf** directory, change the value of **spark.shuffle.manager** in the **spark-defaults.conf** file to **sort**, save the modification, exit, and run the task again.

   .. code-block::

      spark.shuffle.manager = sort

#. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-50845__en-us_topic_0000002488267400_en-us_topic_0000002157258632_li10360155511379>`.

**Collect fault information.**

3. .. _alm-50845__en-us_topic_0000002488267400_en-us_topic_0000002157258632_li10360155511379:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

4. Expand the **Service** drop-down list, and select **MemArtsStore** for the target cluster.

5. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

6. Contact O&M engineers and send the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
