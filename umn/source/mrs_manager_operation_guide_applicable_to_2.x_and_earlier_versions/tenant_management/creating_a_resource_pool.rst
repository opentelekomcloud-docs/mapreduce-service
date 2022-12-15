:original_name: mrs_01_0544.html

.. _mrs_01_0544:

Creating a Resource Pool
========================

Scenario
--------

In an MRS cluster, users can logically divide Yarn cluster nodes to combine multiple NodeManagers into a Yarn resource pool. Each NodeManager belongs to one resource pool only. The system contains a **Default** resource pool by default. All NodeManagers that are not added to customized resource pools belong to this resource pool.

You can create a customized resource pool on MRS Manager and add hosts that have not been added to other customized resource pools to it.

Procedure
---------

#. On MRS Manager, click **Tenant**.
#. Click the **Resource Pools** tab.
#. Click **Add Resource Pool**.
#. In **Create Resource Pool**, set the properties of the resource pool.

   -  **Name**: Enter a name for the resource pool. The name of the newly created resource pool cannot be **Default**.

      The name consists of 1 to 20 characters and can contain digits, letters, and underscores (_) but cannot start with an underscore (_).

   -  **Hosts**: In the host list on the left, select the name of a specified host and click |image1| to add the selected host to the resource pool. Only hosts in the cluster can be selected. The host list of a resource pool can be left blank.

#. Click **OK**.
#. After a resource pool is created, users can view the **Name**, **Members**, **Type**, **vCore** and **Memory** in the resource pool list. Hosts that are added to the customized resource pool are no longer members of the **Default** resource pool.

.. |image1| image:: /_static/images/en-us_image_0000001349257217.png
