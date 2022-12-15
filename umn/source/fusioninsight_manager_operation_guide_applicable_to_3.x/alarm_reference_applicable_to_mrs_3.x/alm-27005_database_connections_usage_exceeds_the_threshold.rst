:original_name: ALM-27005.html

.. _ALM-27005:

ALM-27005 Database Connections Usage Exceeds the Threshold
==========================================================

Description
-----------

The system checks the usage of the number of database connections of the nodes where DBServer instances are located every 30 seconds and compares the usage with the threshold. If the usage exceeds the threshold for five consecutive times (this number is configurable, and 5 is the default value), the system generates this alarm. The default usage threshold is 90%, and you can configure it based on site requirements.

The trigger count is configurable. This alarm is cleared in the following scenarios:

-  The trigger count is 1, and the usage of the number of database connections is less than or equal to the threshold.
-  The trigger count is greater than 1, and the usage of the number of database connections is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
27005    Major          Yes
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
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

Upper-layer services may fail to connect to the DBService database, affecting services.

Possible Causes
---------------

-  Too many database connections are used.
-  The maximum number of database connections is improperly configured.
-  The alarm threshold or alarm trigger count is improperly configured.

Procedure
---------

**Checking whether too many data connections are used**

#. On FusionInsight Manager, click DBService in the service list on the left navigation pane. The DBService monitoring page is displayed.

#. Observe the number of connections used by the database user, as shown in :ref:`Figure 1 <alm-27005__fig821715142011>`. Based on the service scenario, reduce the number of database user connections.

   .. _alm-27005__fig821715142011:

   .. figure:: /_static/images/en-us_image_0269417469.png
      :alt: **Figure 1** Number of connections used by database users

      **Figure 1** Number of connections used by database users

#. Wait for 2 minutes and check whether the alarm is automatically cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`4 <alm-27005__li96747179515>`.

**Checking whether the maximum number of database connections is properly configured**

4. .. _alm-27005__li96747179515:

   Log in to FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **DBService** > **Configurations**. On the displayed page, select the **All** **Configurations** tab, and increase the maximum number of database connections based on service requirements, as shown in :ref:`Figure 2 <alm-27005__fig1567417179514>`. Click **Save**. In the displayed **Save configuration** dialog box, click **OK**.

   .. _alm-27005__fig1567417179514:

   .. figure:: /_static/images/en-us_image_0000001086795516.png
      :alt: **Figure 2** Setting the maximum number of database connections

      **Figure 2** Setting the maximum number of database connections

5. After the maximum number of database connections is changed, restart DBService (do not restart the upper-layer services).

   Procedure: Log in to FusionInsight Manager and choose **Cluster** > *Name of the desired cluster* > **Services** > **DBService**. On the displayed page, choose **More** > **Restart** **Service**. Enter the password of the current login user and click **OK**. Do not select **Restart upper-layer services.**, click **OK**.

6. After the service is restarted, wait for 2 minutes and check whether the alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`7 <alm-27005__li66961681117>`.

**Checking whether the alarm threshold or trigger count is properly configured**

7. .. _alm-27005__li66961681117:

   Log in to FusionInsight Manager and change the alarm threshold and alarm trigger count based on the actual database connection usage.

   Choose **O&M**> **Alarm** > **Thresholds** > *Name of the desired cluster >* **DBService > Database > Database Connections Usage (DBServer)**. In the **Database Connections Usage (DBServer)** area, click the pencil icon next to **Trigger Count**. In the displayed dialog box, change the trigger count, as shown in :ref:`Figure 3 <alm-27005__fig14885145323516>`.

   .. note::

      **Trigger Count**: If the usage of the number of database connections exceeds the threshold consecutively for more than the value of this parameter, an alarm is generated.

   .. _alm-27005__fig14885145323516:

   .. figure:: /_static/images/en-us_image_0000001133372255.png
      :alt: **Figure 3** Setting alarm trigger count

      **Figure 3** Setting alarm trigger count

   Based on the actual database connection usage, choose **O&M** >\ **Alarm** > **Thresholds** > *Name of the desired cluster* > **DBService > Database > Database Connections Usage (DBServer)**. In the **Database Connections Usage (DBServer)** area, click **Modify** in the **Operation** column. In the **Modify Rule** dialog box, modify the required parameters and click **OK** as shown in :ref:`Figure 4 <alm-27005__fig19690175212407>`.

   .. _alm-27005__fig19690175212407:

   .. figure:: /_static/images/en-us_image_0000001390936180.png
      :alt: **Figure 4** Set alarm threshold

      **Figure 4** Set alarm threshold

8. Wait for 2 minutes and check whether the alarm is automatically cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`9 <alm-27005__li195612031415>`.

**Collect fault information**

9.  .. _alm-27005__li195612031415:

    On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

10. Select **DBService** in the required cluster from the **Service**.

11. Specify the host for collecting logs by setting the **Host** parameter that is optional. By default, all hosts are selected.

12. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

13. Contact the O&M personnel and send the collected fault logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269417473.png
