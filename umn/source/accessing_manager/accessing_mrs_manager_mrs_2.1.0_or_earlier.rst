:original_name: mrs_01_0102.html

.. _mrs_01_0102:

Accessing MRS Manager MRS 2.1.0 or Earlier)
===========================================

Scenario
--------

MRS uses FusionInsight Manager to monitor, configure, and manage clusters. You can access FusionInsight Manager by clicking **Access Manager** on the **Dashboard** tab page of your MRS cluster and entering username **admin** and the password configured during cluster creation on the login page that is displayed.

.. _mrs_01_0102__en-us_topic_0035209594_section1511920110246:

Accessing FusionInsight Manager Using an EIP
--------------------------------------------

#. Log in to the MRS management console.

#. In the navigation pane, choose **Clusters** > **Active Clusters**. Click the target cluster name to access the cluster details page.

#. Click **Access Manager** next to **MRS Manager**. In the displayed dialog box, set **Access Mode** to **EIP**. For details about **Direct Connect**, see :ref:`Access Through Direct Connect <mrs_01_0645>`.

   a. If no EIP is bound during MRS cluster creation, select an available EIP from the drop-down list on the right of **IEP**. If you have bound an EIP when creating a cluster, go to :ref:`3.b <mrs_01_0102__li1362714487427>`.

      .. note::

         If no EIP is available, click **Manage EIP** to create one. Then, select the created EIP from the drop-down list on the right of **EIP**.

   b. .. _mrs_01_0102__li1362714487427:

      Select the security group to which the security group rule to be added belongs. The security group is configured when the cluster is created.

   c. Add a security group rule. By default, your public IP address used for accessing port 9022 is filled in the rule. To enable multiple IP address segments to access MRS Manager, see :ref:`6 <mrs_01_0102__en-us_topic_0035209594_li1049410469610>` to :ref:`9 <mrs_01_0102__en-us_topic_0035209594_li035723593115>`. If you want to view, modify, or delete a security group rule, click **Manage Security Group Rule**.

      .. note::

         -  It is normal that the automatically generated public IP address is different from the local IP address and no action is required.
         -  If port 9022 is a Knox port, you need to enable the permission of port 9022 to access Knox for accessing MRS Manager.

   d. Select the checkbox stating that **I confirm that xx.xx.xx.xx is a trusted public IP address and MRS Manager can be accessed using this IP address**.

#. Click **OK**. The MRS Manager login page is displayed.

#. Enter the default username **admin** and the password set during cluster creation, and click **Log In**. The MRS Manager page is displayed.

#. .. _mrs_01_0102__en-us_topic_0035209594_li1049410469610:

   On the MRS management console, choose **Clusters** > **Active Clusters**, and click the target cluster name to access the cluster details page.

   .. note::

      To assign MRS Manager access permissions to other users, follow instructions from :ref:`6 <mrs_01_0102__en-us_topic_0035209594_li1049410469610>` to :ref:`9 <mrs_01_0102__en-us_topic_0035209594_li035723593115>` to add the users' public IP addresses to the trusted range.

#. Click **Add Security Group Rule** on the right of **EIP**.

#. On the **Add Security Group Rule** page, add the IP address segment for users to access the public network and select **I confirm that the authorized object is a trusted public IP address range. Do not use 0.0.0.0/0. Otherwise, security risks may arise**.

   By default, the IP address used for accessing the public network is filled. You can change the IP address segment as required. To enable multiple IP address segments, repeat steps :ref:`6 <mrs_01_0102__en-us_topic_0035209594_li1049410469610>` to :ref:`9 <mrs_01_0102__en-us_topic_0035209594_li035723593115>`. If you want to view, modify, or delete a security group rule, click **Manage Security Group Rule**.

#. .. _mrs_01_0102__en-us_topic_0035209594_li035723593115:

   Click **OK**.

Accessing MRS Manager Using an ECS
----------------------------------

#. On the MRS management console, click **Clusters**.

#. On the **Active Clusters** page, click the name of the specified cluster.

   Record the **AZ**, **VPC**, and **Security Group** of the cluster.

#. On the ECS management console, create an ECS.

   -  The **AZ**, **VPC**, and **Security Group** of the ECS must be the same as those of the cluster to be accessed.
   -  Select a Windows public image. For example, select the enterprise image **Enterprise_Windows_STD_2012R2_20170316-0(80GB)**.
   -  For details about other configuration parameters, see **Elastic Cloud Server > User Guide > Getting Started > Creating and Logging In to a Windows ECS**.

   .. note::

      If the security group of the ECS is different from **Default Security Group** of the MRS cluster, you can modify the configuration using either of the following methods:

      -  Change the default security group of the ECS to the security group of the MRS cluster. For details, see **Elastic Cloud Server** > **User Guide** > **Security Group** > **Changing a Security Group**.
      -  Add two security group rules to the security groups of the Master and Core nodes to enable the ECS to access the cluster. Set **Protocol** to **TCP** and **ports** of the two security group rules to **28443** and **20009**, respectively. For details, see **Virtual Private Cloud** > **User Guide** > **Security** > **Security Group** > **Adding a Security Group Rule**.

#. On the VPC management console, apply for an EIP and bind it to the ECS.

   For details, see **Virtual Private Cloud** > **User Guide** > **Elastic IP** > **Assigning an EIP and Binding It to an ECS**.

#. Log in to the ECS.

   The Windows system account, password, EIP, and the security group rules are required for logging in to the ECS. For details, see **Elastic Cloud Server > User Guide > Instances > Logging In to a Windows ECS**.

#. On the Windows remote desktop, use your browser to access Manager.

   For example, you can use Internet Explorer 11 in the Windows 2012 OS.

   The Manager access address is in the format of **https://**\ *Cluster Manager IP Address*\ **:28443/web**. Enter the name and password of the MRS cluster user, for example, user **admin**.

   .. note::

      -  To obtain the cluster manager IP address, remotely log in to the Master2 node, and run the **ifconfig** command. In the command output, **eth0:wsom** indicates the cluster manager IP address. Record the value of **inet**. If the cluster manager IP address cannot be queried on the Master2 node, switch to the Master1 node to query and record the cluster manager IP address. If there is only one Master node, query and record the cluster manager IP address of the Master node.
      -  If you access MRS Manager with other MRS cluster usernames, change the password upon your first access. The new password must meet the requirements of the current password complexity policies.
      -  By default, a user is locked after inputting an incorrect password five consecutive times. The user is automatically unlocked after 5 minutes.

#. Log out of FusionInsight Manager. To log out of Manager, move the cursor to |image1| in the upper right corner and click **Log Out**.

Changing an EIP for a Cluster
-----------------------------

#. On the MRS management console, choose **Clusters** > **Active Clusters**, and click the target cluster name to access the cluster details page.

#. View EIPs

#. Log in to the VPC management console.

#. Choose **Elastic IP and Bandwidth** > **EIPs**.

#. Search for the EIP bound to the MRS cluster and click **Unbind** in the **Operation** column to unbind the EIP from the MRS cluster.

   |image2|

#. Log in to the MRS management console, choose **Clusters** > **Active Clusters**, and click the target cluster name to access the cluster details page.

   **EIP** on the cluster details page is displayed as **Unbound**.

#. Click **Access Manager** next to **MRS Manager**. In the displayed dialog box, set **Access Mode** to **EIP**.

#. Select a new EIP from the EIP drop-down list and configure other parameters. For details, see :ref:`Accessing FusionInsight Manager Using an EIP <mrs_01_0102__en-us_topic_0035209594_section1511920110246>`.

Granting the Permission to Access MRS Manager to Other Users
------------------------------------------------------------

#. .. _mrs_01_0102__li1750491811399:

   On the MRS management console, choose **Clusters** > **Active Clusters**, and click the target cluster name to access the cluster details page.

#. Click **Add Security Group Rule** on the right of **EIP**.

#. On the **Add Security Group Rule** page, add the IP address segment for users to access the public network and select **I confirm that the authorized object is a trusted public IP address range. Do not use 0.0.0.0/0. Otherwise, security risks may arise**.

   By default, the IP address used for accessing the public network is filled. You can change the IP address segment as required. To enable multiple IP address segments, repeat steps :ref:`1 <mrs_01_0102__li1750491811399>` to :ref:`4 <mrs_01_0102__li55051218183912>`. If you want to view, modify, or delete a security group rule, click **Manage Security Group Rule**.

#. .. _mrs_01_0102__li55051218183912:

   Click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001349137801.jpg
.. |image2| image:: /_static/images/en-us_image_0000001390878044.png
