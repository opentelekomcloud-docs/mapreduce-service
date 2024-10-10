:original_name: mrs_01_249283.html

.. _mrs_01_249283:

Quickly Creating a Doris Cluster
================================

This section describes how to quickly create a Doris cluster. Doris is a high-performance, real-time analytical database, suitable for report analysis, ad hoc query, and federated data lake query acceleration.

A Doris cluster contains only the Doris 1.2.3 component.


Quickly Creating a Doris Cluster
--------------------------------

#. Log in to the MRS management console.

#. Click **Create Cluster**. The page for creating a cluster is displayed.

#. On the displayed page, click the **Quick Config** tab.

#. Configure basic information as follows. For details about the parameters, see :ref:`Creating a Custom Cluster <mrs_01_0513>`.

   -  **Region**: Retain the default value.
   -  **Cluster Name**: You can use the default name or add the project name initials or dates for distinction, for example, **mrs_20180321**.
   -  **Cluster Type**: Select **Doris Cluster**.
   -  **Cluster Version**: The latest version is selected by default. (Components vary depending on the version type. Select a version type as needed.)
   -  **Component**: Select **Doris Cluster**.
   -  **AZ**: Retain the default value.
   -  **Enterprise Project**: Select the default project.
   -  **VPC**: Retain the default value. If there is no available VPC, click **View VPC** to access the VPC console and create one.
   -  **Subnet**: Retain the default value.
   -  **CPU Architecture**: Use the default value.
   -  **Cluster Nodes**: Set the number of cluster nodes and node specifications based on your needs. For MRS 3.\ *x* and later, the memory of a master node must be at least 64 GB.
   -  **Kerberos Authentication**: Whether to enable Kerberos authentication. This option cannot be changed after you create a cluster.
   -  **Username**: The default value is **root**/**admin**. User **root** is used to remotely log in to ECSs and user **admin** is used to access FusionInsight Manager.
   -  **Password**: Set a password for user **root**/**admin**.
   -  **Confirm Password**: Enter the password of user **root**/**admin** again.

#. Select **Enable** to enable secure communications. For details, see :ref:`Communication Security Authorization <mrs_01_0786>`.

#. Click **Create Now**.

   If Kerberos Authentication is toggled on, the system asks you to confirm whether this function is required. If it is, click **Continue**. If not, click **Back** to disable it and then proceed with the subsequent steps. This option cannot be changed after you create a cluster.

#. Click **Back to Cluster List** to view the cluster status. Click **Access Cluster** to view cluster details.

   For details about cluster status during creation, see the description of the status parameters in :ref:`Table 1 <en-us_topic_0012808230__table3950169215120>`.

   It takes some time to create a cluster. The initial status of the cluster is **Starting**. The cluster status will change to **Running** if the cluster is successfully created.

   On the MRS management console, a maximum of 10 clusters can be created concurrently, and a maximum of 100 clusters can be managed.
