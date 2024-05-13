:original_name: mrs_01_248973.html

.. _mrs_01_248973:

Scaling In ClickHouseServer Nodes
=================================

Before removing ClickHouseServer instance nodes, you need to decommission them. Multiple node replicas of the same shard **must be decommissioned at the same time**. If there is a faulty ClickHouseServer instance node in the cluster, all instance nodes of the cluster cannot be decommissioned. For more constraints, see :ref:`Constraints on ClickHouseServer Scale-in <mrs_01_248972>`.

.. note::

   -  Perform the decommissioning in idle hours because the operation will occupy certain bandwidth resources.
   -  The decommissioning operation can be performed only to ClickHouseServer. ClickHouseBalancer cannot be decommissioned.
   -  **This operation is only supported for MRS 3.1.2-LTS.6 and later.**

#. Use PuTTY to log in to the node where ClickHouseServer is installed as user **root** and run the following command:

   **echo 'select \* from system.clusters' \| curl -k 'https://**\ *IP address of the node where the ClickHouseServer instance is located*\ **:**\ *Port number*\ **/' -u** *ck_user*\ **:**\ *Password* **--data-binary @-**

   Record the nodes of the same shard. In the following command output, the nodes with the same number in bold belong to the same shard.

   .. code-block:: console

      [root@kwephispra44948 ~]# echo 'select * from  system.clusters' | curl -k 'https://10.112.17.189:21422/' -u ck_user:Bigdata_2013  --data-binary @-
      default_cluster 1       1       1       kwephispra44947 10.112.17.150  21427   0                       0       0
      default_cluster 1       1       2       kwephispra44948 10.112.17.189  21427   0                       0       0

   .. note::

      -  To view the port number of ClickHouseServer instance nodes, log in to MRS Manager, choose **Cluster** > **Services** > **ClickHouse**, click **Configuration** > **All Configurations**, and choose **ClickHouseServer (Role)** on the left.

         In security mode (Kerberos authentication enabled), check the value of **https_port**, which is the port of a ClickHouseServer instance node.

         In common mode (Kerberos authentication disabled), check the value of **http_port**, which is the port of a ClickHouseServer instance node.

      -  **ck_user** indicates the created ClickHouse user, which must be bound to a role with the ClickHouse administrator permission. For details about how to create a user and a role, see :ref:`Creating a User <admin_guide_000137>` and :ref:`Managing Roles <admin_guide_000148>`, respectively.

#. Log in to the MRS console and click the cluster name to go to the cluster details page.

#. Click the **Components** tab and click **ClickHouse**. Then switch to **Instances**, select the **ClickHouseServer** instances to be removed, click **More**, and select **Decommission**.

#. Click the **Components** tab and click **ClickHouse**. Then click **More**, and select **Synchronize Configuration**.

#. Click the **Nodes** tab and click the ClickHouseServer instance node that has been decommissioned.

#. On the ECS page, click **Stop**. In the displayed dialog box, select **Forcibly stop the preceding ECSs** and click **Yes**.

#. Go back to the MRS console, click the **Nodes** tab, locate the row that contains the target node group, and click **Scale In** in the **Operation** column to go to the **Scale In** page.

#. Set **Scale-In Type** to **Specific node** and select the node to be removed.

#. Select **I understand the consequences of performing the scale-in operation**. Click **OK**.

#. Click the **Components** tab and check whether each component is normal. If any component is abnormal, wait for 5 to 10 minutes and check the component status again. If the fault persists, contact technical support.

#. Click the **Alarms** tab and check whether there are exception alarms. If there are exception alarms, clear them before performing other operations.
