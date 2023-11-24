:original_name: mrs_01_2354.html

.. _mrs_01_2354:

Quick Creation of a ClickHouse Cluster
======================================

This section describes how to quickly create a ClickHouse cluster. ClickHouse is a columnar database management system used for online analysis. It features the ultimate compression rate and fast query performance. It is widely used in Internet advertisement, app and web traffic analysis, telecom, finance, and IoT fields.

The ClickHouse cluster table engine that uses Kunpeng as the CPU architecture does not support HDFS and Kafka.


Quick Creation of a ClickHouse Cluster
--------------------------------------

#. Log in to the MRS console.

#. Click **Create Cluster**. The page for creating a cluster is displayed.

#. Click the **Quick Config** tab.

#. Configure basic cluster information. For details about the parameters, see :ref:`Creating a Custom Cluster <mrs_01_0513>`.

   -  **Region**: Use the default value.
   -  **Cluster Name**: You can use the default name. However, you are advised to include a project name abbreviation or date for consolidated memory and easy distinguishing, Example: **mrs_20201121**.
   -  **Cluster Version**: Select the latest version, which is the default value. (The components provided by a cluster vary according to the cluster version. Select a cluster version based on site requirements.)
   -  **Component**: Select **ClickHouse cluster**.
   -  **AZ**: Use the default value.
   -  **VPC**: Use the default value. If there is no available VPC, click **View VPC** to access the VPC console and create a new VPC.
   -  **Subnet**: Use the default value.
   -  **Enterprise Project**: Use the default value.
   -  **Cluster Node**: Select the number of cluster nodes and node specifications based on site requirements. For MRS 3.\ *x* or later, the memory of the master node must be greater than 64 GB.
   -  **Kerberos Authentication**: Select whether to enable Kerberos authentication.
   -  **Username**: The default value is **root/admin**. User **root** is used to remotely log in to ECSs, and user **admin** is used to access the cluster management page.
   -  **Password**: Set a password for user **root**/**admin**.
   -  **Confirm Password**: Enter the password of user **root**/**admin** again.

#. Select **Enable** to enable secure communications. For details, see :ref:`Communication Security Authorization <mrs_01_0786>`.

#. **Click Apply Now.**

   If Kerberos authentication is enabled for a cluster, check whether Kerberos authentication is required. If yes, click **Continue**. If no, click **Back** to disable Kerberos authentication and then create a cluster.

#. Click **Back to Cluster List** to view the cluster status. Click **Access Cluster** to view cluster details.

   For details about cluster status during creation, see the description of the status parameters in :ref:`Table 1 <en-us_topic_0012808230__table3950169215120>`.

   It takes some time to create a cluster. The initial status of the cluster is **Starting**. After the cluster has been created successfully, the cluster status becomes **Running**.

   On the MRS management console, a maximum of 10 clusters can be concurrently created, and a maximum of 100 clusters can be managed.
