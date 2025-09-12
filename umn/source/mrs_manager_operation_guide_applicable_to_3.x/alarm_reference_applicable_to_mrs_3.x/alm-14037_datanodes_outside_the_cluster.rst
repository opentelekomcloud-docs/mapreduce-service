:original_name: ALM-14037.html

.. _ALM-14037:

ALM-14037 DataNodes Outside the Cluster
=======================================

This alarm applies only to MRS 3.3.1 or later.

Alarm Description
-----------------

The NameNode checks whether there are DataNodes that are not managed in the cluster every 8 hours. This alarm is generated when there is a DataNode outside the cluster. This alarm is cleared when no DataNode is outside the cluster.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
14037    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------------+---------------------------------------------------------------------------------------------------------------------------+
| Type                   | Parameter         | Description                                                                                                               |
+========================+===================+===========================================================================================================================+
| Location Information   | Source            | Specifies the cluster for which the alarm was generated.                                                                  |
+------------------------+-------------------+---------------------------------------------------------------------------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm was generated.                                                                  |
+------------------------+-------------------+---------------------------------------------------------------------------------------------------------------------------+
|                        | NameServiceName   | Specifies the NameService for which the alarm was generated.                                                              |
+------------------------+-------------------+---------------------------------------------------------------------------------------------------------------------------+
| Additional Information | Trigger Condition | Specifies the alarm triggering condition, that is, the IP address and port of a DataNode outside the cluster is detected. |
+------------------------+-------------------+---------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

Data may be lost.

Possible Causes
---------------

After a host is forcibly deleted, the host is powered on again, and the process is restarted.

Handling Procedure
------------------

#. Log in to MRS Manager, click **O&M**, and choose **Alarm** > **Alarms** to view the alarm details. In the additional information area, check the IP address of the host for which the alarm is generated.
#. Stop the DataNode process on the host for which the alarm is reported.

   .. important::

      If there are multiple IP addresses of the host, you can **stop only one DataNode process at a time** and stop the next DataNode process only after **Number of Blocks to Be Replicated** changes to **0**.

   a. Log in to the host for which the alarm is generated as the **root** user and change the permission on the **hadoop** directory in the installation directory **${BIGDATA_HOME}/FusionInsight_HD_*/install**.

      **chmod 000 ${BIGDATA_HOME}/FusionInsight_HD\_8.1.0.1/install/FusionInsight-Hadoop-3.3.1**

   b. Run the following commands to obtain the PID of the DataNode process and stop it on the host:

      **ps -ef \| grep Dproc_datanode**

      **kill -15** *PID*

   c. Choose **Cluster** > **Services** > **HDFS**. Check the **Basic Information** area in the **Dashboard** tab (or the **NameService Summary** area in the **Dashboard** tab of HDFS), and wait until the value of **Blocks to be Replicated** changes to **0**.

#. Wait for 8 hours and check whether the alarm is cleared and whether the number of blocks to be replicated is 0.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-14037__li6107182982310>`.

**Collect fault information.**

4. .. _alm-14037__li6107182982310:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

5. Expand the drop-down list next to the **Service** field. In the **Services** dialog box that is displayed, select **HDFS** for the target cluster.

6. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

7. Contact O&M personnel and provide the collected logs.
