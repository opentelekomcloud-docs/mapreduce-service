:original_name: admin_guide_000031.html

.. _admin_guide_000031:

Performing Active/Standby Switchover of a Role Instance
=======================================================

Scenario
--------

Some service roles are deployed in active/standby mode. If the active instance needs to be maintained and cannot provide services, or other maintenance is required, you can manually trigger an active/standby switchover.

Procedure
---------

#. Log in to MRS Manager.
#. Choose **Cluster** > *Name of the desired cluster* > **Services**.
#. Click the specified service name on the service management page.
#. On the service details page, expand the **More** drop-down list and select **Perform Role Instance Switchover**.
#. In the displayed dialog box, enter the password of the current login user and click **OK**.
#. In the displayed dialog box, click **OK** to perform active/standby switchover for the role instance.

   .. note::

      -  The Manager component package only supports the active/standby switchover of DBService role instances.
      -  The HD component package supports the active/standby switchover of the following service role instances: HDFS, YARN, Storm, HBase, and MapReduce.
      -  When an active/standby switchover is performed for a NameNode on HDFS, a NameService must be set.
      -  The Porter component package only supports the active/standby switchover of Loader role instances.
      -  This function cannot be used for other role instances.
