:original_name: mrs_01_2394.html

.. _mrs_01_2394:

Changing the Ranger Data Source to LDAP for a Normal Cluster
============================================================

By default, the Ranger data source of the security cluster can be accessed by FusionInsight Manager LDAP users. By default, the Ranger data source of a common cluster can be accessed by Unix users.

Prerequisites
-------------

-  Check whether the cluster is in normal mode.
-  The Ranger component has been installed.

Procedure
---------

#. Log in to the MRS management console.
#. Choose **Clusters** > **Active Clusters**, select a running cluster, and click its name to switch to the cluster details page.
#. Click the **Nodes** tab and select the node group whose **Node Type** is **Master**.
#. Go to the ECS page of the active Master node and click **Remote Login**.

5. Log in to the active Master node as user **root**, go to the **/opt/Bigdata/components/FusionInsight_HD\_8.1.2.2/Ranger** directory, and change the value of **ranger.usersync.sync.source** in the **configurations.xml** file to **ldap**.

   .. code-block::

      ranger.usersync.sync.source
      <value model="NoSec">ldap</value>

6. Run the following commands on the active Master node to restart the controller process:

   **su - omm**

   **sh /opt/Bigdata/om-server\_8.1.2.2/om/sbin/restart-controller.sh**

   .. note::

      When the controller process is restarted, the Manager page cannot be accessed for a short period of time, which is normal. After the controller process is restarted, you can access the MRS Manager page properly.

7. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Clusters** > **Services** > **Ranger**. In the upper right corner of the **Dashboard** page, click **More** and choose **Synchronize Configuration**.

8. On the Ranger instance page, select the **UserSync** instance and choose **More** > **Restart Instance**.

9. On the **Dashboard** page of the Ranger service, click **RangerAdmin** and choose **Settings** > **Users/Groups/Roles** to check whether LDAP users exist.
