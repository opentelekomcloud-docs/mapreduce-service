:original_name: admin_guide_000072.html

.. _admin_guide_000072:

Configuring the Alarm Masking Status
====================================

Scenario
--------

If you do not want FusionInsight Manager to report specified alarms in the following scenarios, you can manually mask the alarms.

-  Some unimportant alarms and minor alarms need to be masked.
-  When a third-party product is integrated with FusionInsight, some alarms of the product are duplicated with the alarms of FusionInsight and need to be masked.
-  When the deployment environment is special, certain alarms may be falsely reported and need to be masked.

After an alarm is masked, new alarms with the same ID as the alarm are neither displayed on the **Alarm** page nor counted. The reported alarms are still displayed.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **O&M** > **Alarm** > **Masking Setting**.

#. In the **Masking Setting** area, select the specified service or module.

#. Select an alarm from the alarm list.


   .. figure:: /_static/images/en-us_image_0000001369953797.png
      :alt: **Figure 1** Masking an alarm

      **Figure 1** Masking an alarm

   The information about the alarm is displayed, including the alarm name, ID, severity, masking status, and operations can be performed on the alarm.

   -  The masking status includes **Display** and **Masking**.
   -  Operations include **Masking** and **Help**.

   .. note::

      You can filter specified alarms based on the masking status and alarm severity.

#. Set the masking status for an alarm:

   -  Click **Masking**. In the displayed dialog box, click **OK** to change the alarm masking status to **Masking**.
   -  Click **Cancel Masking**. In the dialog box that is displayed, click **OK** to change the masking status of the alarm to **Display**.
