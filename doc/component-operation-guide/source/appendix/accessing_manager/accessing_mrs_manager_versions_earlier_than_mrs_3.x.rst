:original_name: mrs_01_0102.html

.. _mrs_01_0102:

Accessing MRS Manager (Versions Earlier Than MRS 3.x)
=====================================================

Scenario
--------

Clusters of versions earlier than MRS 3.x use MRS Manager to monitor, configure, and manage clusters. You can open the MRS Manager page on the MRS console.

Accessing MRS manager
---------------------

#. Log in to the MRS management console.

#. In the navigation pane, choose **Clusters** > **Active Clusters**. Click the target cluster name to access the cluster details page.

#. Click **Access Manager**. The **Access MRS Manager** page is displayed.

   -  If you have bound an EIP when creating a cluster,

      a. Select the security group to which the security group rule to be added belongs. The security group is configured when the cluster is created.
      b. Add a security group rule. By default, your public IP address used for accessing port 9022 is filled in the rule. To enable multiple IP address segments to access MRS Manager, see :ref:`6 <mrs_01_0102__en-us_topic_0264269234_en-us_topic_0035209594_li1049410469610>` to :ref:`9 <mrs_01_0102__en-us_topic_0264269234_en-us_topic_0035209594_li035723593115>`. If you want to view, modify, or delete a security group rule, click **Manage Security Group Rule**.

         .. note::

            -  It is normal that the automatically generated public IP address is different from the local IP address and no action is required.
            -  If port 9022 is a Knox port, you need to enable the permission of port 9022 to access Knox for accessing MRS Manager.

      c. Select the checkbox stating that **I confirm that xx.xx.xx.xx is a trusted public IP address and MRS Manager can be accessed using this IP address**.

   -  If you have not bound an EIP when creating a cluster,

      a. Select an available EIP from the drop-down list or click **Manage EIP** to create one.
      b. Select the security group to which the security group rule to be added belongs. The security group is configured when the cluster is created.
      c. Add a security group rule. By default, your public IP address used for accessing port 9022 is filled in the rule. To enable multiple IP address segments to access MRS Manager, see :ref:`6 <mrs_01_0102__en-us_topic_0264269234_en-us_topic_0035209594_li1049410469610>` to :ref:`9 <mrs_01_0102__en-us_topic_0264269234_en-us_topic_0035209594_li035723593115>`. If you want to view, modify, or delete a security group rule, click **Manage Security Group Rule**.

         .. note::

            -  It is normal that the automatically generated public IP address is different from the local IP address and no action is required.
            -  If port 9022 is a Knox port, you need to enable the permission of port 9022 to access Knox for accessing MRS Manager.

      d. Select the checkbox stating that **I confirm that xx.xx.xx.xx is a trusted public IP address and MRS Manager can be accessed using this IP address**.

#. Click **OK**. The MRS Manager login page is displayed.

#. Enter the default username **admin** and the password set during cluster creation, and click **Log In**. The MRS Manager page is displayed.

#. .. _mrs_01_0102__en-us_topic_0264269234_en-us_topic_0035209594_li1049410469610:

   On the MRS console, click **Clusters** and choose **Active Clusters**. Click the target cluster name to access the cluster details page.

   .. note::

      To assign MRS Manager access permissions to other users, follow instructions from :ref:`6 <mrs_01_0102__en-us_topic_0264269234_en-us_topic_0035209594_li1049410469610>` to :ref:`9 <mrs_01_0102__en-us_topic_0264269234_en-us_topic_0035209594_li035723593115>` to add the users' public IP addresses to the trusted range.

#. Click **Add Security Group Rule** on the right of **EIP**.

#. On the **Add Security Group Rule** page, add the IP address segment for users to access the public network and select **I confirm that the authorized object is a trusted public IP address range. Do not use 0.0.0.0/0. Otherwise, security risks may arise**.

   By default, the IP address used for accessing the public network is filled. You can change the IP address segment as required. To enable multiple IP address segments, repeat steps :ref:`6 <mrs_01_0102__en-us_topic_0264269234_en-us_topic_0035209594_li1049410469610>` to :ref:`9 <mrs_01_0102__en-us_topic_0264269234_en-us_topic_0035209594_li035723593115>`. If you want to view, modify, or delete a security group rule, click **Manage Security Group Rule**.

#. .. _mrs_01_0102__en-us_topic_0264269234_en-us_topic_0035209594_li035723593115:

   Click **OK**.

If the cluster version is **MRS 1.7.2** and earlier and Kerberos authentication is not enabled for the cluster, perform the following operations:

#. Log in to the MRS management console.

#. In the navigation pane, click **Clusters** and choose **Active Clusters**. Click the target cluster name to access the cluster details page.

#. Click **Access MRS Manager**.

   After logging in to the MRS management console, you can access MRS Manager. By default, user **admin** is used for login. You do not need to enter the password again.

If the cluster version is **MRS 1.7.2** or earlier and Kerberos authentication is enabled for the cluster, see **Accessing Web Pages of Open Source Components Managed in MRS Clusters** > **Access Using a Windows ECS** in the *MapReduce Service User Guide*.

Granting the Permission to Access MRS Manager to Other Users
------------------------------------------------------------

#. .. _mrs_01_0102__en-us_topic_0264269234_li1750491811399:

   On the MRS console, click **Clusters** and choose **Active Clusters**. Click the target cluster name to access the cluster details page.

#. Click **Add Security Group Rule** on the right of **EIP**.

#. On the **Add Security Group Rule** page, add the IP address segment for users to access the public network and select.\ **I confirm that the authorized object is a trusted public IP address range. Do not use 0.0.0.0/0. Otherwise, security risks may arise.**

   By default, the IP address used for accessing the public network is filled. You can change the IP address segment as required. To enable multiple IP address segments, repeat steps :ref:`1 <mrs_01_0102__en-us_topic_0264269234_li1750491811399>` to :ref:`4 <mrs_01_0102__en-us_topic_0264269234_li55051218183912>`. If you want to view, modify, or delete a security group rule, click **Manage Security Group Rule**.

#. .. _mrs_01_0102__en-us_topic_0264269234_li55051218183912:

   Click **OK**.
