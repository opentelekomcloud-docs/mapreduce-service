:original_name: admin_guide_000127.html

.. _admin_guide_000127:

Adding a Resource Pool
======================

Scenario
--------

In a cluster, you can logically group Yarn NodeManagers into Yarn resource pools. Each NodeManager belongs to only one resource pool. You can create a custom resource pool on MRS Manager and add the hosts that have not been added to any custom resource pools to this resource pool so that specified queues can use the computing resources provided by these hosts.

The system contains a **default** resource pool by default. All NodeManagers that are not added to custom resource pools belong to this resource pool.

Procedure
---------

#. Log in to MRS Manager.

#. Choose **Tenant Resources** > **Resource Pool**.

#. Click **Add Resource Pool**.

#. Set resource pool attributes.

   -  **Cluster**: Select the cluster to which the resource pool is to be added.
   -  **Name**: Enter the name of the resource pool. The name contains 1 to 50 characters, including digits, letters, and underscores (_), and cannot start with an underscore (_).
   -  **Resource Label**: Enter the resource label of the resource pool. The value can contain 1 to 50 characters, including digits, letters, underscores (_), and hyphens (-), and must start with a digit or letter.
   -  **Resource**: In the **Available Hosts** area, select specified hosts and click |image1| to add the hosts to the **Selected Hosts** area. Only hosts in the cluster can be selected. The host list in the resource pool can be left blank.

      .. note::

         You can filter hosts by host name, number of CPU cores, memory, operating system, or platform type based on service requirements.

#. Click **OK**.

   After the resource pool is created, you can view its name, members, and mode in the resource pool list. Hosts that are added to the custom resource pool are no longer members of the **default** resource pool.

.. |image1| image:: /_static/images/en-us_image_0000001392733930.png
