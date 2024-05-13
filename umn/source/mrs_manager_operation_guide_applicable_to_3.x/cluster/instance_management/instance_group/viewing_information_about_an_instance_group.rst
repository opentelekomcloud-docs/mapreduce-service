:original_name: admin_guide_000047.html

.. _admin_guide_000047:

Viewing Information About an Instance Group
===========================================

Scenario
--------

The cluster administrator can view the instance group of a specified service on MRS Manager.

Procedure
---------

#. Log in to MRS Manager.
#. Choose **Cluster** > *Name of the desired cluster* > **Services**.
#. Click the specified service name on the service management page.
#. On the displayed page, click the **Instance Groups** tab.
#. In the navigation tree, select a role. On the **Basic** tab page, view all instances in the instance group.

   .. note::

      To move an instance from an instance group to another, perform the following operations:

      a. Select the instance to be moved and click **Move**.

      b. In the displayed dialog box, select an instance group to which the instance to be moved.

         During the migration, the configuration of the new instance group is automatically inherited. If the instance configuration is modified before the migration, the configuration of the instance prevails.

      c. Click **OK**.

         Restart the expired service or instance for the configuration to take effect.
