:original_name: ALM-14009.html

.. _ALM-14009:

ALM-14009 Number of Dead DataNodes Exceeds the Threshold
========================================================

Description
-----------

The system periodically detects the number of dead DataNodes in the HDFS cluster every 30 seconds, and compares the number with the threshold. The number of DataNodes in the Dead state has a default threshold. This alarm is generated when the number exceeds the threshold.

You can change the threshold in **O&M** > **Alarm >** **Thresholds** > *Name of the desired cluster* **>** **HDFS**.

When the **Trigger Count** is 1, this alarm is cleared when the number of Dead DataNodes is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the number of Dead DataNodes is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
14009    Major          Yes
======== ============== =====================

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
| NameServiceName   | Specifies the NameService for which the alarm is generated.                                                                  |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

DataNodes that are in the Dead state cannot provide HDFS services.

Possible Causes
---------------

-  DataNodes are faulty or overloaded.
-  The network between the NameNode and the DataNode is disconnected or busy.
-  NameNodes are overloaded.
-  The NameNodes are not restarted after the DataNode is deleted.

Procedure
---------

**Check whether DataNodes are faulty.**

#. On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS**. The **HDFS Status** page is displayed.

#. In the **Basic Information** area, click **NameNode(Active)** to go to the HDFS WebUI.

   .. note::

      By default, the **admin** user does not have the permissions to manage other components. If the page cannot be opened or the displayed content is incomplete when you access the native UI of a component due to insufficient permissions, you can manually create a user with the permissions to manage that component.

#. On the HDFS WebUI, click the **Datanodes** tab. In the **In operation** area, click **Filter** to check whether **down** is in the drop-down list.

   -  If yes, select **down**, record the information about the filtered DataNodes, and go to :ref:`4 <alm-14009__li4499900717545>`.
   -  If no, go to :ref:`8 <alm-14009__li2034924617545>`.

#. .. _alm-14009__li4499900717545:

   On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* > **Services** > **HDFS** > **Instance** to check whether recorded DataNodes exist in the instance list.

   -  If all recorded DataNodes exist, go to :ref:`5 <alm-14009__li22951519113013>`.
   -  If none of the recorded DataNodes exists, go to :ref:`6 <alm-14009__li4226377546>`.
   -  If some of the recorded DataNodes exist, go to :ref:`7 <alm-14009__li992618717545>`.

#. .. _alm-14009__li22951519113013:

   Locate the DataNode instance, click **More** > **Restart Instance** to restart it and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-14009__li2034924617545>`.

#. .. _alm-14009__li4226377546:

   Select all NameNode instances, choose **More** > **Instance Rolling Restart** to restart them and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`16 <alm-14009__li4607504917545>`.

#. .. _alm-14009__li992618717545:

   Select all NameNode instances, choose **More** > **Instance Rolling Restart** to restart them. Locate the DataNode instance, click **More** > **Restart Instance** to restart it and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-14009__li2034924617545>`.

**Check the status of the network between the NameNode and the DataNode.**

8. .. _alm-14009__li2034924617545:

   Log in to the faulty DataNode on the management page as user **root**, and run the **ping** *IP address of the NameNode* command to check whether the network between the DataNode and the NameNode is abnormal.

   On the FusionInsight Manager page, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Instance**. In the instance list, view the service plane IP address of the faulty DataNode.

   -  If yes, go to :ref:`9 <alm-14009__li3193609617545>`.
   -  If no, go to :ref:`10 <alm-14009__li4029888217545>`.

9. .. _alm-14009__li3193609617545:

   Rectify the network fault, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-14009__li4029888217545>`.

**Check whether the DataNode is overloaded.**

10. .. _alm-14009__li4029888217545:

    On the FusionInsight Manager portal, choose **O&M > Alarm > Alarms** and check whether the alarm **ALM-14008 HDFS DataNode Memory Usage Exceeds the Threshold** exists.

    -  If yes, go to :ref:`11 <alm-14009__li3775267317545>`.
    -  If no, go to :ref:`13 <alm-14009__li2641038017545>`.

11. .. _alm-14009__li3775267317545:

    See **ALM-14008 HDFS DataNode Memory Usage Exceeds the Threshold** to handle the alarm and check whether the alarm is cleared.

    -  If yes, go to :ref:`12 <alm-14009__li4983258617545>`.
    -  If no, go to :ref:`13 <alm-14009__li2641038017545>`.

12. .. _alm-14009__li4983258617545:

    Check whether the alarm is cleared from the alarm list.

    -  If yes, no further action is required.
    -  If no, go to :ref:`13 <alm-14009__li2641038017545>`.

**Check whether the NameNode is overloaded.**

13. .. _alm-14009__li2641038017545:

    On the FusionInsight Manager portal, choose **O&M > Alarm > Alarms** and check whether the alarm **ALM-14007 HDFS NameNode Memory Usage Exceeds the Threshold** exists.

    -  If yes, go to :ref:`14 <alm-14009__li1070095917545>`.
    -  If no, go to :ref:`16 <alm-14009__li4607504917545>`.

14. .. _alm-14009__li1070095917545:

    See **ALM-14007 HDFS NameNode Memory Usage Exceeds the Threshold** to handle the alarm and check whether the alarm is cleared.

    -  If yes, go to :ref:`15 <alm-14009__li5612534017545>`.
    -  If no, go to :ref:`16 <alm-14009__li4607504917545>`.

15. .. _alm-14009__li5612534017545:

    Check whether the alarm is cleared from the alarm list.

    -  If yes, no further action is required.
    -  If no, go to :ref:`16 <alm-14009__li4607504917545>`.

**Collect fault information.**

16. .. _alm-14009__li4607504917545:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

17. Select **HDFS** in the required cluster from the **Service**.

18. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

19. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532767590.png
