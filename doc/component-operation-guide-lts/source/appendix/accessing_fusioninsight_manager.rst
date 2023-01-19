:original_name: mrs_01_2124.html

.. _mrs_01_2124:

Accessing FusionInsight Manager
===============================

Scenario
--------

FusionInsight Manager is used to monitor, configure, and manage clusters. After the cluster is installed, you can use the account to log in to FusionInsight Manager.

Currently, you can access FusionInsight Manager using the following methods:

-  :ref:`Accessing FusionInsight Manager Using EIP <mrs_01_2124__en-us_topic_0000001219029417_en-us_topic_0000001173471140_section17594144112487>`
-  :ref:`Accessing FusionInsight Manager Using Direct Connect <mrs_01_2124__en-us_topic_0000001219029417_en-us_topic_0000001173471140_section12101164416719>`
-  :ref:`Accessing FusionInsight Manager from an ECS <mrs_01_2124__en-us_topic_0000001219029417_en-us_topic_0000001173471140_section20880102283115>`

You can switch the access methods between **EIP** and **Direct Connect** on the MRS console by performing the following steps:

Log in to the MRS console and click the target cluster to go its details page. In the **Basic Information** area, click |image1| on the right of **Access Manager**.

.. note::

   If you cannot log in to the WebUI of the component, access FusionInsight Manager by referring to :ref:`Accessing FusionInsight Manager from an ECS <mrs_01_2124__en-us_topic_0000001219029417_en-us_topic_0000001173471140_section20880102283115>`.

.. _mrs_01_2124__en-us_topic_0000001219029417_en-us_topic_0000001173471140_section17594144112487:

Accessing FusionInsight Manager Using EIP
-----------------------------------------

#. Log in to the MRS management console.

#. In the navigation pane, choose **Clusters** > **Active Clusters**. Click the target cluster name to access the cluster details page.

#. Click **Manager** next to **MRS Manager**. In the displayed dialog box, configure the EIP information.

   a. If no EIP is bound during MRS cluster creation, select an available EIP from the EIP drop-down list or click **Manage EIP** to create an EIP. If you have bound an EIP when creating a cluster, go to :ref:`3.b <mrs_01_2124__en-us_topic_0000001219029417_en-us_topic_0000001173471140_li59591846143810>`.

   b. .. _mrs_01_2124__en-us_topic_0000001219029417_en-us_topic_0000001173471140_li59591846143810:

      Select the security group to which the security group rule to be added belongs. The security group is configured when the cluster is created.

   c. Add a security group rule. By default, the filled-in rule is used to access the EIP. To enable multiple IP address segments to access Manager, see steps :ref:`6 <mrs_01_2124__en-us_topic_0000001219029417_en-us_topic_0000001173471140_en-us_topic_0035209594_li1049410469610>` to :ref:`9 <mrs_01_2124__en-us_topic_0000001219029417_en-us_topic_0000001173471140_en-us_topic_0035209594_li035723593115>`. If you want to view, modify, or delete a security group rule, click **Manage Security Group Rule**.

   d. Select the information to be confirmed and click **OK**.

#. Click **OK**. The Manager login page is displayed.

#. Enter the default username **admin** and the password set during cluster creation, and click **Log In**. The Manager page is displayed.

#. .. _mrs_01_2124__en-us_topic_0000001219029417_en-us_topic_0000001173471140_en-us_topic_0035209594_li1049410469610:

   On the MRS management console, choose **Clusters** > **Active Clusters**. Click the target cluster name to access the cluster details page.

   .. note::

      To grant other users the permission to access Manager, perform :ref:`6 <mrs_01_2124__en-us_topic_0000001219029417_en-us_topic_0000001173471140_en-us_topic_0035209594_li1049410469610>` to :ref:`9 <mrs_01_2124__en-us_topic_0000001219029417_en-us_topic_0000001173471140_en-us_topic_0035209594_li035723593115>` to add the users' public IP addresses to the trusted IP address range.

#. Click **Add Security Group Rule** on the right of **EIP**.

#. On the **Add Security Group Rule** page, add the IP address segment for users to access the public network and select **I confirm that the authorized object is a trusted public IP address range. Do not use 0.0.0.0/0. Otherwise, security risks may arise.**

   By default, the IP address used for accessing the public network is filled. You can change the IP address segment as required. To enable multiple IP address segments, repeat steps :ref:`6 <mrs_01_2124__en-us_topic_0000001219029417_en-us_topic_0000001173471140_en-us_topic_0035209594_li1049410469610>` to :ref:`9 <mrs_01_2124__en-us_topic_0000001219029417_en-us_topic_0000001173471140_en-us_topic_0035209594_li035723593115>`. If you want to view, modify, or delete a security group rule, click **Manage Security Group Rule**.

#. .. _mrs_01_2124__en-us_topic_0000001219029417_en-us_topic_0000001173471140_en-us_topic_0035209594_li035723593115:

   Click **OK**.

.. _mrs_01_2124__en-us_topic_0000001219029417_en-us_topic_0000001173471140_section12101164416719:

Accessing FusionInsight Manager by Using Direct Connect
-------------------------------------------------------

When **Direct Connect** is enabled in the environment, you can access FusionInsight Manager by using Direct Connect as an system administrator.

#. Log in to the MRS management console.
#. In the navigation pane, choose **Clusters** > **Active Clusters**. Click the target cluster name to access the cluster details page.
#. Click **Access Manager** next to **MRS Manager**. In the displayed dialog box, select **Direct Connect**.
#. Click **OK**. The Manager login page is displayed.
#. Enter the default username **admin** and the password set during cluster creation, and click **Log In**. The Manager page is displayed.

.. _mrs_01_2124__en-us_topic_0000001219029417_en-us_topic_0000001173471140_section20880102283115:

Accessing FusionInsight Manager from an ECS
-------------------------------------------

#. On the MRS management console, click **Clusters**.

#. On the **Active Clusters** page, click the name of the specified cluster.

   Record the **AZ**, **VPC**, **MRS Manager**\ **Security Group** of the cluster.

#. On the homepage of the management console, choose **Service List** > **Elastic Cloud Server** to switch to the ECS management console and create an ECS.

   -  The **AZ**, **VPC**, and **Security Group** of the ECS must be the same as those of the cluster to be accessed.
   -  Select a Windows public image. For example, a standard image **Windows Server 2012 R2 Standard 64bit(40GB)**.
   -  For details about other configuration parameters, see **Elastic Cloud Server > User Guide > Getting Started > Creating and Logging In to a Windows ECS**.

   .. note::

      If the security group of the ECS is different from **Default Security Group** of the Master node, you can modify the configuration using either of the following methods:

      -  Change the security group of the ECS to the default security group of the Master node. For details, see **Elastic Cloud Server** > **User Guide** > **Security Group** > **Changing a Security Group**.
      -  Add two security group rules to the security groups of the Master and Core nodes to enable the ECS to access the cluster. Set **Protocol** to **TCP**, **Ports** of the two security group rules to **28443** and **20009**, respectively. For details, see **Virtual Private Cloud > User Guide > Security > Security Group > Adding a Security Group Rule**.

#. On the VPC management console, apply for an EIP and bind it to the ECS.

   For details, see **Virtual Private Cloud** > **User Guide** > **Elastic IP** > **Assigning an EIP and Binding It to an ECS**.

#. Log in to the ECS.

   The Windows system account, password, EIP, and the security group rules are required for logging in to the ECS. For details, see **Elastic Cloud Server > User Guide > Instances > Logging In to a Windows ECS**.

#. On the Windows remote desktop, use your browser to access Manager.

   For example, you can use Internet Explorer 11 in the Windows 2012 OS.

   The address for accessing Manager is the address of the MRS Manager page. Enter the name and password of the cluster user, for example, user **admin**.

   |image2|

   .. note::

      -  If you access Manager with other cluster usernames, change the password upon your first access. The new password must meet the requirements of the current password complexity policies. For details, contact the system administrator.
      -  By default, a user is locked after inputting an incorrect password five consecutive times. The user is automatically unlocked after 5 minutes.

#. Log out of FusionInsight Manager. To log out of Manager, move the cursor to |image3| in the upper right corner and click **Log Out**.

.. |image1| image:: /_static/images/en-us_image_0000001295900152.png
.. |image2| image:: /_static/images/en-us_image_0000001388357306.png
.. |image3| image:: /_static/images/en-us_image_0000001438277693.png
