:original_name: mrs_01_0497.html

.. _mrs_01_0497:

Quick Creation of a Kafka Streaming Cluster
===========================================

This section describes how to quickly create a Kafka streaming cluster. The Kafka cluster uses the Kafka and Storm components to provide an open-source messaging system with high throughput and scalability. It is widely used in scenarios such as log collection and monitoring data aggregation to implement efficient streaming data collection and real-time data processing and storage.


Quick Creation of a Kafka Streaming Cluster
-------------------------------------------

#. Log in to the MRS console.

#. Click **Create Cluster**. The page for creating a cluster is displayed.

#. Click the **Quick Config** tab.

#. Configure basic cluster information. For details about the parameters, see :ref:`Creating a Custom Cluster <mrs_01_0513>`.

   -  **Region**: Use the default value.
   -  **Cluster Name**: You can use the default name. However, you are advised to include a project name abbreviation or date for consolidated memory and easy distinguishing, for example, **mrs_20200321**.
   -  **Cluster Version**: The components provided by a cluster vary according to the cluster version. Select a cluster version based on site requirements.
   -  **Component**: Select **Kafka streaming cluster**.
   -  **AZ**: Use the default value.
   -  **VPC**: Use the default value. If there is no available VPC, click **View VPC** to access the VPC console and create a new VPC.
   -  **Subnet**: Use the default value.
   -  **Enterprise Project**: Use the default value.
   -  **Cluster Node**: Select the number of cluster nodes and node specifications based on site requirements. For MRS 3.\ *x* or later, the memory of the master node must be greater than 64 GB.
   -  **Cluster HA**: Use the default value. This parameter is not available in MRS 3.\ *x*.
   -  **Kerberos Authentication**: Select whether to enable Kerberos authentication.
   -  **Username**: The default username is **admin**, which is used to log in to MRS Manager.
   -  **Password**: Set a password for user **admin**.
   -  **Confirm Password**: Enter the password of user **admin** again.
   -  **Key Pair**: Select a key pair from the drop-down list to log in to an ECS. Select **"I acknowledge that I have obtained private key file** *SSHkey-xxx* **and that without this file I will not be able to log in to my ECS.**" If you have never created a key pair, click **View Key Pair** to create or import a key pair. And then, obtain a private key file.

#. Select **Enable** to enable secure communications. For details, see :ref:`Communication Security Authorization <mrs_01_0786>`.

#. **Click Apply Now.**

   If Kerberos authentication is enabled for a cluster, check whether Kerberos authentication is required. If yes, click **Continue**. If no, click **Back** to disable Kerberos authentication and then create a cluster.

#. Click **Back to Cluster List** to view the cluster status. Click **Access Cluster** to view cluster details.

   For details about cluster status during creation, see the description of the status parameters in :ref:`Table 1 <en-us_topic_0012808230__table3950169215120>`.

   It takes some time to create a cluster. The initial status of the cluster is **Starting**. After the cluster has been created successfully, the cluster status becomes **Running**.

   On the MRS management console, a maximum of 10 clusters can be concurrently created, and a maximum of 100 clusters can be managed.
