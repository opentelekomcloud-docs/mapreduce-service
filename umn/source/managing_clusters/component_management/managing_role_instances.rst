:original_name: mrs_01_0207.html

.. _mrs_01_0207:

Managing Role Instances
=======================

Scenario
--------

You can start a role instance that is in the **Stopped**, **Failed to stop** or **Failed to start** status, stop an unused or abnormal role instance or restart an abnormal role instance to recover its functions.

Prerequisites
-------------

You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

#. On the MRS cluster details page, click **Components**.

   .. note::

      For versions earlier than MRS 1.7.2, see :ref:`Managing Role Instances <mrs_01_0249>`.

#. Select the target service from the service list.
#. Click the **Instances** tab.
#. Select the check box on the left of the target role instance.
#. Click **More**, select operations such as **Start Instance**, **Stop Instance**, **Restart Instance**, **Rolling-restart Instance**, or **Delete Instance** based on site requirements.
