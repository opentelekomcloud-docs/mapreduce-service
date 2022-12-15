:original_name: mrs_01_0209.html

.. _mrs_01_0209:

Synchronizing Role Instance Configuration
=========================================

Scenario
--------

When **Configuration Status** of a role instance is **Configuration expired** or **Configuration failed**, you can synchronize the configuration data of the role instance with the background configuration.

Impact on the System
--------------------

After synchronizing a role instance configuration, you need to restart the role instance whose configuration has expired. The role instance is unavailable during restart.

Prerequisites
-------------

You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

#. On the MRS cluster details page, click **Components**.

   .. note::

      For versions earlier than MRS 1.7.2, see :ref:`Synchronizing Role Instance Configuration <mrs_01_0251>`.

#. Select a service name.
#. Click the **Instances** tab.
#. Click the target role instance from the role instance list.
#. Choose **More** > **Synchronize Configuration** above the role instance status and indicator information.
#. In the dialog box that is displayed, select **Restart the service or instances whose configurations have expired** and click **Yes** to restart the role instance.
