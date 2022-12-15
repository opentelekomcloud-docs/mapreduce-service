:original_name: alm_26052.html

.. _alm_26052:

ALM-26052 Number of Available Supervisors in Storm Is Lower Than the Threshold
==============================================================================

Description
-----------

The system checks the number of supervisors every 60 seconds and compares it with the threshold. This alarm is generated if the number of supervisors is lower than the threshold.

To modify the threshold, users can choose **System** > **Threshold Configuration** on MRS Manager.

This alarm is cleared if the number of supervisors is greater than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
26052    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------------------------------+
| Parameter         | Description                                                                         |
+===================+=====================================================================================+
| ServiceName       | Specifies the service for which the alarm is generated.                             |
+-------------------+-------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| Trigger Condition | Generates an alarm when the actual indicator value exceeds the specified threshold. |
+-------------------+-------------------------------------------------------------------------------------+

Impact on the System
--------------------

-  Existing tasks in the cluster cannot be executed.
-  The cluster can receive new Storm tasks but cannot execute them.

Possible Causes
---------------

Supervisors are abnormal in the cluster.

Procedure
---------

#. Check the supervisor status.

   a. Go to the cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. Choose **Storm** > **Supervisor**.

   c. In **Role**, check whether the cluster has supervisor instances that are in the **Faulty** or **Recovering** state.

      -  If yes, go to :ref:`1.d <alm_26052__en-us_topic_0191813898_li65587069184020>`.
      -  If no, go to :ref:`2 <alm_26052__en-us_topic_0191813898_li572522141314>`.

   d. .. _alm_26052__en-us_topic_0191813898_li65587069184020:

      Select the supervisor instances that are in the **Faulty** or **Recovering** state and choose **More** > **Restart Instance**.

      -  If yes, go to :ref:`1.e <alm_26052__en-us_topic_0191813898_li52566748184020>`.
      -  If the restart fails, go to :ref:`2 <alm_26052__en-us_topic_0191813898_li572522141314>`.

   e. .. _alm_26052__en-us_topic_0191813898_li52566748184020:

      Wait 30 seconds and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_26052__en-us_topic_0191813898_li572522141314>`.

#. .. _alm_26052__en-us_topic_0191813898_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Related Information
-------------------

N/A
