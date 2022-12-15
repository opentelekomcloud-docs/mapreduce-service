:original_name: ALM-14012.html

.. _ALM-14012:

ALM-14012 JournalNode Is Out of Synchronization
===============================================

Description
-----------

On the active NameNode, the system checks the data consistency of all JournalNodes in the cluster every 5 minutes. This alarm is generated when the data on a JournalNode is inconsistent with the data on the other JournalNodes.

This alarm is cleared in 5 minutes after the data on JournalNodes is consistent.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
14012    Major          Yes
======== ============== =====================

Parameters
----------

+-----------------+-------------------------------------------------------------+
| Name            | Meaning                                                     |
+=================+=============================================================+
| Source          | Specifies the cluster for which the alarm is generated.     |
+-----------------+-------------------------------------------------------------+
| ServiceName     | Specifies the service for which the alarm is generated.     |
+-----------------+-------------------------------------------------------------+
| RoleName        | Specifies the role for which the alarm is generated.        |
+-----------------+-------------------------------------------------------------+
| HostName        | Specifies the host for which the alarm is generated.        |
+-----------------+-------------------------------------------------------------+
| NameServiceName | Specifies the NameService for which the alarm is generated. |
+-----------------+-------------------------------------------------------------+

Impact on the System
--------------------

When a JournalNode is working incorrectly, the data on the node becomes inconsistent with that on the other JournalNodes. If data on more than half of JournalNodes is inconsistent, the NameNode cannot work correctly, making the HDFS service unavailable.

Possible Causes
---------------

-  The JournalNode instance does not exist (deleted or migrated).
-  The JournalNode instance has not been started or has been stopped.
-  The JournalNode instance is working incorrectly.
-  The network of the JournalNode is unreachable.

Procedure
---------

**Check whether the JournalNode instance has been started up.**

#. On the FusionInsight Manager portal, choose **O&M > Alarm > Alarms**. In the alarm list, click the alarm.

#. Check **Location** and obtain the IP address of the JournalNode for which the alarm is generated.

#. Choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Instance**. In the instance list, check whether the JournalNode instance exists on the node for which the alarm is generated.

   -  If yes, go to :ref:`5 <alm-14012__li15222114643411>`.
   -  If no, go to :ref:`4 <alm-14012__li184781433124215>`.

#. .. _alm-14012__li184781433124215:

   Choose **O&M** > **Alarm** > **Alarms**. In the alarm list, click **Clear** in the **Operation** column of the alarm. In the dialog box that is displayed, click **OK**. No further action is needed.

#. .. _alm-14012__li15222114643411:

   Click the JournalNode instance and check whether its **Configuration Status** is **Synchronized**.

   -  If yes, go to :ref:`8 <alm-14012__li28800798973>`.
   -  If no, go to :ref:`6 <alm-14012__li40718266973>`.

#. .. _alm-14012__li40718266973:

   Select the JournalNode instance and choose **Start Instance** to start the instance.

#. After 5 minutes, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`15 <alm-14012__li43402084973>`.

**Check whether the JournalNode instance is working correctly.**

8.  .. _alm-14012__li28800798973:

    Check whether **Running Status** of the JournalNode instance is **Normal**.

    -  If yes, go to :ref:`11 <alm-14012__li3722637973>`.
    -  If no, go to :ref:`9 <alm-14012__li57816175973>`.

9.  .. _alm-14012__li57816175973:

    Select the JournalNode instance and choose **More** > **Restart Instance** to start the instance.

10. After 5 minutes, check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`15 <alm-14012__li43402084973>`.

**Check whether the network of the JournalNode is reachable.**

11. .. _alm-14012__li3722637973:

    On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Instance** to check the service IP address of the active NameNode.

12. Log in to the active NameNode as user **root**.

13. Run the **ping** command to check whether a timeout occurs or the network is unreachable between the active NameNode and the JournalNode.

    **ping** *service IP address of the JournalNode*

    -  If yes, go to :ref:`14 <alm-14012__li25467007973>`.
    -  If no, go to :ref:`15 <alm-14012__li43402084973>`.

14. .. _alm-14012__li25467007973:

    Contact the network administrator to rectify the network fault and check whether the alarm is cleared 5 minutes later.

    -  If yes, no further action is required.
    -  If no, go to :ref:`15 <alm-14012__li43402084973>`.

**Collect fault information.**

15. .. _alm-14012__li43402084973:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

16. Select **HDFS** in the required cluster from the **Service**.

17. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

18. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383967.png
