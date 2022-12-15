:original_name: mrs_01_0647.html

.. _mrs_01_0647:

Access Using a Windows ECS
==========================

MRS allows you to access the web UIs of open-source components through a Windows ECS. This method is complex and is recommended for MRS clusters that do not support the EIP function (security clusters with Kerberos authentication enabled in versions earlier than MRS 1.9.2).

#. On the MRS management console, click **Clusters**.

#. On the **Active Clusters** page, click the name of the specified cluster.

   On the cluster details page, record the **AZ**, **VPC**, **Cluster Manager IP Address**, and **Security Group** of the cluster.

   .. note::

      To obtain the cluster manager IP address, remotely log in to the Master2 node, and run the **ifconfig** command. In the command output, **eth0:wsom** indicates the cluster manager IP address. Record the value of **inet**. If the cluster manager IP address cannot be queried on the Master2 node, switch to the Master1 node to query and record the cluster manager IP address. If there is only one Master node, query and record the cluster manager IP address of the Master node.

#. On the ECS management console, create an ECS.

   -  The **AZ**, **VPC**, and **Security Group** of the ECS must be the same as those of the cluster to be accessed.
   -  Select a Windows public image. For example, select the enterprise image **Enterprise_Windows_STD_2012R2_20170316-0(80GB)**.
   -  For details about other configuration parameters, see **Elastic Cloud Server > User Guide > Getting Started > Creating and Logging In to a Windows ECS**.

   .. note::

      If the security group of the ECS is different from **Security Group** of the MRS cluster, you can modify the configuration using either of the following methods:

      -  Change the security group of the ECS to the security group of the MRS cluster. For details, see **Elastic Cloud Server** > **User Guide** > **Security Group** > **Changing a Security Group**.
      -  Add two security group rules to the security groups of the Master and Core nodes to enable the ECS to access the cluster. Set **Protocol** to **TCP** and **ports** of the two security group rules to **28443** and **20009**, respectively. For details, see **Virtual Private Cloud** > **User Guide** > **Security** > **Security Group** > **Adding a Security Group Rule**.

#. On the VPC management console, apply for an EIP and bind it to the ECS.

   For details, see **Virtual Private Cloud** > **User Guide** > **Elastic IP** > **Assigning an EIP and Binding It to an ECS**.

#. Log in to the ECS.

   The Windows system account, password, EIP, and the security group rules are required for logging in to the ECS. For details, see **Elastic Cloud Server > User Guide > Instances > Logging In to a Windows ECS**.

#. On the Windows remote desktop, use your browser to access Manager.

   For example, you can use Internet Explorer 11 in the Windows 2012 OS.

   The MRS Manager access address is in the format of **https://Cluster Manager IP Address:28443/web**. Enter the name and password of the MRS cluster user, for example, user **admin**.

   .. note::

      -  To obtain the cluster manager IP address, remotely log in to the Master2 node, and run the **ifconfig** command. In the command output, **eth0:wsom** indicates the cluster manager IP address. Record the value of **inet**. If the cluster manager IP address cannot be queried on the Master2 node, switch to the Master1 node to query and record the cluster manager IP address. If there is only one Master node, query and record the cluster manager IP address of the Master node.
      -  If you access MRS Manager with other MRS cluster usernames, change the password upon your first access. The new password must meet the requirements of the current password complexity policies.
      -  By default, a user is locked after inputting an incorrect password five consecutive times. The user is automatically unlocked after 5 minutes.

#. Visit the web UIs of the open-source components by referring to the addresses listed in :ref:`Web UIs of Open Source Components <mrs_01_0362>`.

Related Tasks
-------------

**Configuring the Mapping Between Cluster Node Names and IP Addresses**

#. Log in to MRS Manager, and choose **Host Management**.

   Record the host names and management IP addresses of all nodes in the cluster.

#. In the work environment, use Notepad to open the **hosts** file and add the mapping between node names and IP addresses to the file.

   Fill in one row for each mapping relationship, as shown in the following figure.

   .. code-block::

      192.168.4.127 node-core-Jh3ER
      192.168.4.225 node-master2-PaWVE
      192.168.4.19 node-core-mtZ81
      192.168.4.33 node-master1-zbYN8
      192.168.4.233 node-core-7KoGY

   Save the modifications.
