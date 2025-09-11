:original_name: ALM-14038.html

.. _ALM-14038:

ALM-14038 Router Heap Memory Usage Exceeds the Threshold
========================================================

Alarm Description
-----------------

The system checks the size of the used HDFS Router heap memory and the maximum size of the heap memory that can be allocated every 30 seconds, calculates the ratio of the used heap memory to the maximum size of the heap memory that can be allocated to obtain the heap memory usage, and compares the actual heap memory usage of the HDFS Router with the threshold. The HDFS Router Heap Memory usage has a default threshold. This alarm is generated when the HDFS Router Heap Memory usage exceeds the threshold.

You can change the threshold in **O&M** > **Alarm >** **Thresholds** > *Name of the desired cluster* **>** **HDFS**.

The alarm is cleared when the heap memory usage is less than or equal to the threshold.

Alarm Attributes
----------------

+-----------------------+-----------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                    | Auto Cleared          |
+=======================+===================================+=======================+
| 14038                 | Critical (default threshold: 95%) | Yes                   |
|                       |                                   |                       |
|                       | Major (default threshold: 90%)    |                       |
+-----------------------+-----------------------------------+-----------------------+

Alarm Parameters
----------------

+------------------------+-------------------+---------------------------------------------------------+
| Type                   | Parameter         | Description                                             |
+========================+===================+=========================================================+
| Location Information   | Source            | Specifies the cluster for which the alarm is generated. |
+------------------------+-------------------+---------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm is generated. |
+------------------------+-------------------+---------------------------------------------------------+
|                        | RoleName          | Specifies the role for which the alarm is generated.    |
+------------------------+-------------------+---------------------------------------------------------+
|                        | HostName          | Specifies the host for which the alarm is generated.    |
+------------------------+-------------------+---------------------------------------------------------+
| Additional Information | Trigger Condition | Specifies the alarm triggering condition.               |
+------------------------+-------------------+---------------------------------------------------------+

Impact on the System
--------------------

The HDFS Router Heap Memory usage is too high, which affects the data read/write performance of the HDFS.

Possible Causes
---------------

The HDFS Router Heap Memory is insufficient.

Handling Procedure
------------------

#. On MRS Manager, choose **Cluster** > **Services** > **Ranger** > **Instance** > **PolicySync**. Click **Instance Configuration** and then **All Configurations**, and choose **PolicySync** > **System**.
#. On the MRS Manager portal, choose **Cluster >** **Services** > **HDFS** > **Configurations** > **All Configurations**. In **Search**, enter **GC_OPTS** to check the GC_OPTS memory parameter of **HDFS->Router**.
#. Increase the values of **-Xms** and **-Xmx** in the **GC_OPTS** parameter based on the site requirements and save the configuration.

   .. note::

      If this alarm is generated, the heap memory configured for Router cannot meet the requirements of the current process. You are advised to change the values of **-Xms** and **-Xmx** in the **GC_OPTS** parameter to twice the size of the used heap memory or change the values based on the site requirements.

#. Restart the affected services or instances and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-14038__en-us_topic_0000001973076798_li42224042151734>`.

**Collect fault information.**

5. .. _alm-14038__en-us_topic_0000001973076798_li42224042151734:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **HDFS** for the target cluster.

7. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
