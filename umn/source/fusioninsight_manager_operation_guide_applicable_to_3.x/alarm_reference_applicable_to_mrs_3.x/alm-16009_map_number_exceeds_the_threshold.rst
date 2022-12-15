:original_name: ALM-16009.html

.. _ALM-16009:

ALM-16009 Map Number Exceeds the Threshold
==========================================

Description
-----------

The system checks the number of HQL maps in every 30 seconds. This alarm is generated if the number exceeds the threshold. By default, **Trigger Count** is set to **3**, and the threshold is 5000.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
16009    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

If the number of HQL maps executed on Hive is excessively large, the HQL execution speed is slow, and a large number of resources are occupied.

Possible Causes
---------------

The HQL statements are not the optimal.

Procedure
---------

**Check the number of HQL maps.**

#. On FusionInsight Manager portal, choose **Cluster** >\ *Name of the desired cluster* > **Services** > **Hive** > **Resource**. Check the HQL statements with the excessively large number (5000 or more) of maps in **HQL Map Count**.

2. Locate the corresponding HQL statements, optimize them and execute them again.
3. Check whether the alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`4 <alm-16009__li1284813578408>`.

**Collect fault information.**

4. .. _alm-16009__li1284813578408:

   On the FusionInsight Manager, choose **O&M** > **Log > Download**.

5. Select **Hive** in the required cluster from the **Service**.

6. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

7. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269417385.png
