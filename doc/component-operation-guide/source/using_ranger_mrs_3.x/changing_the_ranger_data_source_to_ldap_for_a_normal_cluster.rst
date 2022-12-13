:original_name: mrs_01_2394.html

.. _mrs_01_2394:

Changing the Ranger Data Source to LDAP for a Normal Cluster
============================================================

By default, the Ranger data source of the security cluster can be accessed by FusionInsight Manager LDAP users. By default, the Ranger data source of a common cluster can be accessed by Unix users.

Prerequisites
-------------

-  The cluster is in normal mode.
-  The Ranger component has been installed.

Procedure
---------

#. Log in to the MRS console.
#. Choose **Clusters** > **Active Clusters**, select a running cluster, and click its name to go to its details page.
#. Click the **Nodes** tab. On the **Nodes** tab page that is displayed, expand the node group whose **Node Type** is **Master**.
#. Go to the ECS page of the active master node and click **Remote Login**.

5. Log in to a master node as user **root**, go to the **/opt/Bigdata/components/FusionInsight_HD\_8.1.0.1/Ranger** directory, and change the values of **ranger.usersync.sync.source** and **ranger.usersync.cookie.enabled** in the **configurations.xml** file to **ldap** and **false**, respectively.

   .. code-block::

      <name>ranger.usersync.sync.source</name>
      <value model="Sec">ldap</value>
      <value model="NoSec">ldap</value>

   .. code-block::

      <name>ranger.usersync.cookie.enabled</name>
      <value>false</value>

   .. note::

      **Change the value of this parameter on all master nodes.**

6. Run the following commands on the active Master node to restart the controller process:

   **su - omm**

   **sh /opt/Bigdata/om-server\_8.1.0.1/om/sbin/restart-controller.sh**

   .. note::

      During controller restart, Manager becomes inaccessible temporarily. After the restart is complete, Manager can be accessed properly.

7. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`. Choose **Cluster** > **Services** > **Ranger**. In the upper right corner of the **Dashboard** page, click **More** and choose **Synchronize Configuration**.

8. On the Ranger instance page, select the **UserSync** instance and choose **More** > **Restart Instance**.

9. On the **Dashboard** page of the Ranger service, click **RangerAdmin** and choose **Settings** > **Users/Groups/Roles** to check whether LDAP users exist.
