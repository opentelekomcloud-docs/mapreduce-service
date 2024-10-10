:original_name: ALM-25007.html

.. _ALM-25007:

ALM-25007 Number of SlapdServer Connections Exceeds the Threshold
=================================================================

Alarm Description
-----------------

The system checks the number of process connections on the SlapdServer node every 30 seconds and compares the actual number with the threshold. This alarm is generated when the number of process connections exceeds the threshold (**1000** by default) for multiple times (**5** by default).

Its **Trigger Count** is configurable. If **Trigger Count** is set to **1**, this alarm is cleared when the number of process connections is less than or equal to the threshold. If **Trigger Count** is greater than **1**, this alarm is cleared when the number of process connections is less than or equal to 90% of the threshold.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
25007    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+-------------------+---------------------------------------------------------+
| Parameter         | Description                                             |
+===================+=========================================================+
| Source            | Specifies the cluster for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.       |
+-------------------+---------------------------------------------------------+

Impact on the System
--------------------

Processes respond slowly or do not work.

Possible Causes
---------------

-  There are too many SlapdServer connections.
-  The alarm threshold or alarm trigger count is improperly configured.

Handling Procedure
------------------

**Check whether there are too many SlapdServer process connections.**

#. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **LdapServer**.

#. On the LdapServer dashboard page, observe the SlapdServer process connections and decrease the connections based on service requirements.


   .. figure:: /_static/images/en-us_image_0000001971659216.png
      :alt: **Figure 1** SlapdServer process connections

      **Figure 1** SlapdServer process connections

#. Wait about 2 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-25007__li1860517366397>`.

**Check whether the alarm threshold or alarm trigger count is properly configured.**

4. .. _alm-25007__li1860517366397:

   On FusionInsight Manager, choose **O&M** > **Alarm** > **Thresholds**, click the name of the desired cluster, choose **LdapServer** > **Other** > **SlapdServer Service Connections**, and check whether the alarm trigger count and alarm threshold are set properly.

   -  If yes, go to :ref:`7 <alm-25007__li2086435114014>`.
   -  If no, go to :ref:`5 <alm-25007__li20605336193916>`.

5. .. _alm-25007__li20605336193916:

   Change the trigger count and alarm threshold based on the actual number of process connections, and apply the changes.

6. Wait 2 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-25007__li2086435114014>`.

**Collect fault information.**

7.  .. _alm-25007__li2086435114014:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Expand the **Service** drop-down list, and select **LdapServer** for the target cluster.

9.  Specify **Hosts** for collecting logs, which is optional. By default, all hosts are selected.

10. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000001971818984.png
