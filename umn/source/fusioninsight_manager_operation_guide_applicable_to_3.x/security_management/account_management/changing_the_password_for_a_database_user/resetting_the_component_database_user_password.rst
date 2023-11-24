:original_name: admin_guide_000363.html

.. _admin_guide_000363:

Resetting the Component Database User Password
==============================================

Scenario
--------

Default passwords for components in the MRS cluster to connect to the DBService database are random. You are advised to periodically reset the passwords of component database users to improve system O&M security.

.. note::

   This section applies only to MRS 3.1.2-LTS.6 or later. For versions earlier than MRS 3.1.2-LTS.6, see :ref:`Changing the Password for a Component Database User <admin_guide_000261>`.

Impact on the System
--------------------

To reset passwords, you need to stop and then restart services, during which services are unavailable.

Procedure
---------

#. On FusionInsight Manager, click **Cluster**, click the name of the desired cluster, and click **Services**.

#. Click the name of the service whose database user password is to be reset, for example, **Kafka**, and click **Stop Service** on the **Dashboard** page.

   In the displayed dialog box, enter the password of the current login user and click **OK**.

   After confirming the impact of stopping the service, wait until the service is stopped.

#. On the **Dashboard** page, choose **More** > **Reset Database Password**.

   In the displayed dialog box, enter the password of the current login user and click **OK**.

   Select "I have read the information and understand the impact", and click **OK**.

#. After the password is reset, click **Start Service** on the **Dashboard** page.

#. In the displayed dialog box, click **OK** and wait until the service is started.
