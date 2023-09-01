:original_name: ALM-45616.html

.. _ALM-45616:

ALM-45616 CDL Job Execution Exception
=====================================

Description
-----------

The system checks whether a CDL job is normal every 60 seconds. This alarm is reported when the CDL job is abnormal. This alarm is cleared when the job is restored or stopped.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45616    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+---------------------------------------------------------------------+
| Name        | Meaning                                                             |
+=============+=====================================================================+
| Source      | Specifies the cluster for which the alarm is generated.             |
+-------------+---------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.             |
+-------------+---------------------------------------------------------------------+
| JobName     | Specifies the job for which the alarm is generated.                 |
+-------------+---------------------------------------------------------------------+
| Username    | Specifies the username of the job for which the alarm is generated. |
+-------------+---------------------------------------------------------------------+

Impact on the System
--------------------

This alarm has no impact on the system.

Possible Causes
---------------

The CDL task fails to be executed due to incorrect parameter settings or other reasons. On the **Job Management** page of the CDL web UI, locate the row where the job is located and click **Failed**/**Abnormal running** in the **Status** column to view the failure cause, or view the failure cause in the logs.

Procedure
---------

#. Log in to FusionInsight Manager as a user who has the CDL job creation or administrator permission.

#. .. _alm-45616__li7271425123815:

   Choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**, click |image1| in the row where **Alarm ID** is **45616**, and view the name of the job for which this alarm is generated in **Location**.

#. Choose **Cluster** > **Services** > **CDL** and click the link next to **CDLService UI** to go to the CDL web UI.

#. Locate the row where the failed job is located based on the job name obtained in :ref:`2 <alm-45616__li7271425123815>`, and click **Abnormal running** or **Failed** in the **Status** column.

   |image2|

#. On the page that is displayed, view the error information and rectify the fault. For example, :ref:`Figure 1 <alm-45616__fig1327218258386>` shows that the task running on Yarn is manually killed. For details, see trace error information, as shown in :ref:`Figure 2 <alm-45616__fig16272152503813>`.

   .. _alm-45616__fig1327218258386:

   .. figure:: /_static/images/en-us_image_0000001582807901.png
      :alt: **Figure 1** CDL job exception

      **Figure 1** CDL job exception

   .. _alm-45616__fig16272152503813:

   .. figure:: /_static/images/en-us_image_0000001532927626.png
      :alt: **Figure 2** Trace error information

      **Figure 2** Trace error information

#. Rectify the fault based on the error information, execute the task again, and check whether the task can be executed successfully.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-45616__li52711725153817>`.

**Collect the fault information.**

7.  .. _alm-45616__li52711725153817:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Select **CDL** in the required cluster for **Service**.

9.  Click |image3| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

After the job is successfully restored or stopped, the alarm is cleared if it has been reported.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927849.png
.. |image2| image:: /_static/images/en-us_image_0000001532767690.png
.. |image3| image:: /_static/images/en-us_image_0000001583127597.png
