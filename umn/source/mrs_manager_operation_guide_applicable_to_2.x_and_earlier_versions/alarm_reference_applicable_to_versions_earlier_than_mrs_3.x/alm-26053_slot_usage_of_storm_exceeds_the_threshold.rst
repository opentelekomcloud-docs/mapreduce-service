:original_name: alm_26053.html

.. _alm_26053:

ALM-26053 Slot Usage of Storm Exceeds the Threshold
===================================================

Description
-----------

The system checks the slot usage of Storm every 60 seconds and compares it with the threshold. This alarm is generated if the slot usage exceeds the threshold.

To modify the threshold, users can choose **System** > **Threshold Configuration** on MRS Manager.

This alarm is cleared if the slot usage is lower than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
26053    Major          Yes
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
| Trigger condition | Generates an alarm when the actual indicator value exceeds the specified threshold. |
+-------------------+-------------------------------------------------------------------------------------+

Impact on the System
--------------------

Users cannot run new Storm tasks.

Possible Causes
---------------

-  Supervisors are abnormal in the cluster.
-  Supervisors are normal but have poor processing capability.

Procedure
---------

#. Check the supervisor status.

   a. Go to the cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. Choose **Storm** > **Supervisor**.

   c. In **Role**, check whether the cluster has supervisor instances that are in the **Faulty** or **Recovering** state.

      -  If yes, go to :ref:`1.d <alm_26053__en-us_topic_0191813942_li6671657118374>`.
      -  If no, go to :ref:`2.a <alm_26053__en-us_topic_0191813942_li142406612228>` or :ref:`3.a <alm_26053__en-us_topic_0191813942_li22838295183633>`.

   d. .. _alm_26053__en-us_topic_0191813942_li6671657118374:

      Select the supervisor instances that are in the **Faulty** or **Recovering** state and choose **More** > **Restart Instance**.

      -  If yes, go to :ref:`1.e <alm_26053__en-us_topic_0191813942_li5198268318374>`.
      -  If the restart fails, go to :ref:`4 <alm_26053__en-us_topic_0191813942_li572522141314>`.

   e. .. _alm_26053__en-us_topic_0191813942_li5198268318374:

      Wait a moment and then check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.a <alm_26053__en-us_topic_0191813942_li142406612228>` or :ref:`3.a <alm_26053__en-us_topic_0191813942_li22838295183633>`.

#. Increase the number of slots for the supervisors.

   a. .. _alm_26053__en-us_topic_0191813942_li142406612228:

      Go to the cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. Choose **Storm** > **Supervisor** > **Service Configuration**, and set **Type** to **All**.

   c. Increase the value of **supervisor.slots.ports** to increase the number of slots for each supervisor. Then restart the instances.

   d. Wait a moment and then check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_26053__en-us_topic_0191813942_li572522141314>`.

#. Expand the capacity of the supervisors.

   a. .. _alm_26053__en-us_topic_0191813942_li22838295183633:

      Add nodes.

   b. Wait a moment and then check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If the restart fails, go to :ref:`4 <alm_26053__en-us_topic_0191813942_li572522141314>`.

#. .. _alm_26053__en-us_topic_0191813942_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Related Information
-------------------

N/A
