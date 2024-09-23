:original_name: mrs_01_0496.html

.. _mrs_01_0496:

Quick Creation of an HBase Analysis Cluster
===========================================

This section describes how to quickly create an HBase query cluster. The HBase cluster uses Hadoop and HBase components to provide a column-oriented distributed cloud storage system featuring enhanced reliability, excellent performance, and elastic scalability. It applies to the storage and distributed computing of massive amounts of data. You can use HBase to build a storage system capable of storing TB- or even PB-level data. With HBase, you can filter and analyze data with ease and get responses in milliseconds, rapidly mining data value.


Quick Creation of an HBase Analysis Cluster
-------------------------------------------

#. Log in to the MRS console.

#. Click **Create Cluster**. The page for creating a cluster is displayed.

#. Click the **Quick Config** tab.

#. Configure basic cluster information. For details about the parameters, see :ref:`Creating a Custom Cluster <mrs_01_0513>`.

   -  **Region**: Use the default value.
   -  **Cluster Name**: You can use the default name. However, you are advised to include a project name abbreviation or date for consolidated memory and easy distinguishing, for example, **mrs_20180321**.
   -  **Cluster Type**: Use the default value.
   -  **Cluster Version**: Select the latest version, which is the default value. (The components provided by a cluster vary according to the cluster version. Select a cluster version based on site requirements.)
   -  **Component**: Select **HBase Query Cluster**.
   -  **AZ**: Use the default value.
   -  **VPC**: Use the default value. If there is no available VPC, click **View VPC** to access the VPC console and create a new VPC.
   -  **Subnet**: Use the default value.
   -  **Enterprise Project**: Use the default value.
   -  **CPU Architecture**: Use the default value.
   -  **Cluster Nodes**: Select the number of cluster nodes and node specifications based on site requirements. For MRS 3.\ *x* or later, the memory of the master node must be greater than 64 GB.
   -  **Kerberos Authentication**: Select whether to enable Kerberos authentication.
   -  **Username**: The default value is **root/admin**. User **root** is used to remotely log in to ECSs, and user **admin** is used to access the cluster management page.
   -  **Password**: Set a password for user **root**/**admin**.
   -  **Confirm Password**: Enter the password of user **root**/**admin** again.

#. Select **Enable** to enable secure communications. For details, see :ref:`Communication Security Authorization <mrs_01_0786>`.

#. **Click Create Now.**

   If Kerberos authentication is enabled for a cluster, check whether Kerberos authentication is required. If yes, click **Continue**. If no, click **Back** to disable Kerberos authentication and then create a cluster.

#. Click **Back to Cluster List** to view the cluster status. Click **Access Cluster** to view cluster details.

   For details about cluster status during creation, see the description of the status parameters in :ref:`Table 1 <en-us_topic_0012808230__table3950169215120>`.

   It takes some time to create a cluster. The initial status of the cluster is **Starting**. After the cluster has been created successfully, the cluster status becomes **Running**.

   On the MRS management console, a maximum of 10 clusters can be concurrently created, and a maximum of 100 clusters can be managed.
