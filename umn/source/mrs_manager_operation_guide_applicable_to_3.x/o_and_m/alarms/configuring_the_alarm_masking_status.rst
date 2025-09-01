:original_name: admin_guide_000072.html

.. _admin_guide_000072:

Configuring the Alarm Masking Status
====================================

Masking an Alarm
----------------

If you do not want MRS Manager to report specified alarms in the following scenarios, you can manually mask the alarms.

-  Some unimportant alarms and minor alarms need to be masked.
-  When a third-party product is integrated with MRS, some alarms of the product are duplicated with the alarms of MRS and need to be masked.
-  When the deployment environment is special, certain alarms may be falsely reported and need to be masked.

After an alarm is masked, new alarms with the same ID as the alarm are neither displayed on the **Alarm** page nor counted. The reported alarms are still displayed.

#. Log in to MRS Manager.

#. Choose **O&M** > **Alarm** > **Masking Setting**.

#. In the **Masking Setting** area, select the specified service or module.

#. Select an alarm from the alarm list.


   .. figure:: /_static/images/en-us_image_0000001392733962.png
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

.. _admin_guide_000072__section57034286161:

Configuring Alarm Masking and Alarm Trigger Count
-------------------------------------------------

.. note::

   This operation is available in clusters of MRS 3.5.0 or later only.

The MRS allows you to mask alarms and number of trigger times on the background. If the number of alarm report times is less than or equal to the number of alarm trigger times, no alarm will be reported.

#. Log in to the active OMS node as user **omm** using PuTTY.

#. .. _admin_guide_000072__li276225016712:

   Run the following command to modify the **alarm_filter_config.json** configuration file. If the file does not exist, create it.

   **vi $BIGDATA_HOME/om-server/OMS/workspace/conf/fms/alarm_filter_config.json**

#. .. _admin_guide_000072__li146742521575:

   Configure or add parameters based on service demands.

   -  **Alarm ID**: ID of the alarm to be masked, for example, **12016**.
   -  **is_filtered:** Whether to mask the alarm. **true** indicates that the alarm is masked and not reported. **false** indicates that the alarm is reported after certain times of trigger.
   -  **smoothing_times**: trigger count. If the number of alarm trigger times is less than or equal to the value of this parameter, no alarm will be reported. The value is an integer greater than 0.

   The **is_filtered** parameter takes priority over the **smoothing_times** parameter.

   For example, if the configuration is as follows, alarm 12016 is masked and alarm 12017 is reported after it is triggered for more than three times:

   .. code-block::

      {
        "12016": {
          "is_filtered": true,
          "smoothing_times": 1
        },
        "12017": {
          "is_filtered": false,
          "smoothing_times": 3
        }
      }

#. Restart the FMS service on the active OMS node as user **omm** to apply the configuration.

   **sh $BIGDATA_HOME/om-server/OMS/workspace/bin/omm_s_fm_ctl.sh restart**

#. Log in to the active OMS node as user **omm** using PuTTY. Perform steps :ref:`2 <admin_guide_000072__li276225016712>` and :ref:`3 <admin_guide_000072__li146742521575>`.
