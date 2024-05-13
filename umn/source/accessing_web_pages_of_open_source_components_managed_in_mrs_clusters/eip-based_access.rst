:original_name: mrs_01_0646.html

.. _mrs_01_0646:

EIP-based Access
================

You can bind an EIP to a cluster to access the web UIs of the open-source components managed in the MRS cluster. This method is simple and easy to use and is recommended for accessing the web UIs of the open-source components.

Binding an EIP to a Cluster and Adding a Security Group Rule
------------------------------------------------------------

#. On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users. After the IAM users are synchronized, the **Components** tab is available.
#. Click **Access Manager** on the right of **MRS Manager**.
#. The page for accessing MRS Manager is displayed. Bind an EIP and add a security group rule. Perform the following operations only when you access the web UIs of the open-source components of the cluster for the first time.

   a. Select an available EIP from the EIP drop-down list to bind it. If there is no available EIP, click **Manage EIP** to create an EIP. If an EIP has been bound during cluster creation, skip this step.
   b. Select the security group to which the security group rule to be added belongs. The security group is configured when the group is created.
   c. Add a security group rule. By default, your public IP address used for accessing port 9022 is filled in the rule. If you want to view, modify, or delete a security group rule, click **Manage Security Group Rule**.

      .. note::

         -  It is normal that the automatically generated public IP address is different from the local IP address and no action is required.
         -  If port 9022 is a Knox port, you need to enable the permission of port 9022 to access Knox for accessing MRS components.

   d. Select the checkbox stating that **I confirm that xx.xx.xx.xx is a trusted public IP address and MRS Manager can be accessed using this IP address**.
   e. Click **OK**. The login page is displayed. Enter the username **admin** and the password set during cluster creation.

#. Log in to MRS Manager and choose **Cluster** > **Services** > **HDFS**. On the displayed page, click **NameNode(**\ *Host name*\ **, active)** to access the HDFS web UI. The HDFS NameNode is used as an example. For details about the web UIs of other components, see :ref:`Web UIs of Open Source Components <mrs_01_0362>`.
