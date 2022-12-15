:original_name: mrs_01_0251.html

.. _mrs_01_0251:

Synchronizing Role Instance Configuration
=========================================

Scenario
--------

When **Configuration Status** of a role instance is **Expired** or **Failed**, you can synchronize the configuration data of the role instance with the background configuration.

Impact on the System
--------------------

After synchronizing a role instance configuration, you need to restart the role instance whose configuration has expired. The role instance is unavailable during restart.

Procedure
---------

#. On MRS Manager, click **Services** and select a service name.

#. Click the **Instances** tab.

#. Click the target role instance from the role instance list.

#. Choose **More** > **Synchronize Configuration** above the role instance status and indicator information.

#. In the displayed dialog box, select **Restart services and instances whose configuration have expired**, and click **OK** to restart the role instance.

   After **Operation successful** is displayed, click **Finish**. The role instance is started successfully.
