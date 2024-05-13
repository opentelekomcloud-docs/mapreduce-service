:original_name: ALM-38007.html

.. _ALM-38007:

ALM-38007 Status of Kafka Default User Is Abnormal
==================================================

Description
-----------

The system checks the default user of Kafka every 60 seconds. This alarm is generated when the system detects that the user status is abnormal.

**Trigger Count** is set to **1**. This alarm is cleared when the user status becomes normal.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
38007    Critical       Yes
======== ============== =====================

Parameters
----------

+-------------------+-------------------------------------------------------------------------+
| Name              | Meaning                                                                 |
+===================+=========================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                 |
+-------------------+-------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                 |
+-------------------+-------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                    |
+-------------------+-------------------------------------------------------------------------+
| HostName          | Specifies the host name for which the alarm is generated.               |
+-------------------+-------------------------------------------------------------------------+
| Trigger Condition | Specifies the condition that the Kafka default user status is abnormal. |
+-------------------+-------------------------------------------------------------------------+

Impact on the System
--------------------

If the Kafka default user status is abnormal, metadata synchronization between Brokers and interaction between Kafka and ZooKeeper will be affected, affecting service production, consumption, and topic creation and deletion.

Possible Causes
---------------

-  The Sssd service is abnormal.
-  Some Broker instances stop running.

Procedure
---------

**Check whether the Sssd service is abnormal.**

#. On the MRS Manager portal, choose **O&M** > **Alarm** > **Alarms** > **Status of Kafka Default User Is Abnormal** > **Location** to check the host name of the instance for which the alarm is generated.

#. Find the host information in the alarm information and log in to the host.

#. Run the **id -Gn kafka** command and check whether "No such user" is displayed in the command output.

   -  If yes, record the host name of the node and go to :ref:`4 <alm-38007__li1465202115440>`.
   -  If no, go to :ref:`6 <alm-38007__li14809510142018>`.

#. .. _alm-38007__li1465202115440:

   On the MRS Manager home page, choose **O&M** > **Alarm** > **Alarms**. Check whether there is **Sssd Service Exception** in the alarm information. If there is, handle the alarm based on alarm information.

**Check the running status of the Broker instance.**

5. On the MRS Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Instance**. The Kafka instance page is displayed.

6. .. _alm-38007__li14809510142018:

   Check whether there are stopped nodes on all Broker instances.

   -  If yes, go to :ref:`7 <alm-38007__li9809111022018>`.
   -  If no, go to :ref:`8 <alm-38007__li4809151011206>`.

7. .. _alm-38007__li9809111022018:

   Select all stopped Broker instances and click **Start Instance**.

8. .. _alm-38007__li4809151011206:

   Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-38007__li783366415440>`.

**Collect fault information.**

9.  .. _alm-38007__li783366415440:

    On MRS Manager, choose **O&M** > **Log** > **Download**.

10. In the **Service** area, select **Kafka** in the required cluster.

11. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807621.png
