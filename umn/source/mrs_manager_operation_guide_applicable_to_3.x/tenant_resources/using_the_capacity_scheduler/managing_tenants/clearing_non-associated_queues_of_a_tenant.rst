:original_name: admin_guide_000125.html

.. _admin_guide_000125:

Clearing Non-associated Queues of a Tenant
==========================================

Scenario
--------

If Yarn uses the Capacity scheduler, deleting a tenant only sets the queue capacity of the tenant to **0** and the tenant status to **STOPPED** but does not clear the queues of the tenant in Yarn. Limited by the Yarn mechanism, queues cannot be dynamically deleted. You can run commands to manually delete residual queues.

Impact on the System
--------------------

-  During the script execution, the Controller service is restarted, Yarn configurations are synchronized, and the active and standby ResourceManagers are restarted.
-  MRS Manager becomes inaccessible during the restart of the Controller service.
-  After the active and standby ResourceManagers are restarted, an alarm is generated indicating that Yarn and components that depend on Yarn are temporarily unavailable.

Prerequisites
-------------

Queues of a deleted tenant still exist.

Procedure
---------

#. Check that queues of the deleted tenant still exist.

   a. On MRS Manager, choose **Cluster**, click the name of the target cluster, and choose **Services** > **Yarn**. Click the link of the active ResourceManager in **ResourceManager WebUI** to go to the ResourceManager web UI.
   b. Click **Scheduler** in the navigation tree on the left. In the right pane, you can view that queues of the tenant still exist in the **STOPPED** state and their **Configured Capacity** is **0**.

#. Log in to the active management node as user **omm**.

#. Switch the directory and execute the **cleanQueuesAndRestartRM.sh** script.

   **cd ${BIGDATA_HOME}/om-server/om/sbin**

   **./cleanQueuesAndRestartRM.sh** **-c** *Cluster ID*

   .. note::

      You can choose **Cluster**, click the cluster name, and choose **Cluster Properties** on MRS Manager to view the cluster ID.

   During the script execution, you need to enter **yes** and the password.

   .. code-block::

      Running the script will restart Controller and restart ResourceManager.
      Are you sure you want to continue connecting (yes/no)?yes
      Please input admin password:
      Begin to backup queues ...
      ...

#. After the script is executed successfully, log in to MRS Manager, choose **Cluster**, click the cluster name, and choose **Services** > **Yarn**. Click the link of the active ResourceManager in **ResourceManager WebUI** to go to the ResourceManager web UI.

#. Click **Scheduler** in the navigation tree on the left. In the right pane, you can view that queues of the tenant have been cleared.
