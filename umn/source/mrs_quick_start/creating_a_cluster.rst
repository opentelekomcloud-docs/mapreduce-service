:original_name: mrs_01_0027.html

.. _mrs_01_0027:

Creating a Cluster
==================

The first step of using MRS is to create a cluster. This section describes how to create a cluster on the MRS management console.

Procedure
---------

#. Log in to the MRS console.

#. Click **Create Cluster**, the **Create Cluster** page is displayed

   .. note::

      When creating a cluster, pay attention to quota notification. If a resource quota is insufficient, increase the resource quota as prompted and create a cluster.

#. On the page for create a cluster, click the **Custom Config** tab.

#. Configure cluster software information.

   -  **Region**: Use the default value.
   -  **Cluster Name**: You can use the default name. However, you are advised to include a project name abbreviation or date for consolidated memory and easy distinguishing, for example, **mrs_20180321**.
   -  **Cluster Version**: Select the latest version, which is the default value.
   -  **Cluster Type**: Use the default **Analysis Cluster**.
   -  **Component Port**: Use the default **Open source**.
   -  **Component**: Select components such as Spark2x, HBase, and Hive for the analysis cluster. For a streaming cluster, select components such as Kafka and Storm. For a hybrid cluster, you can select the components of the analysis cluster and streaming cluster based on service requirements.

#. Click **Next**.

   -  **AZ**: Use the default value.
   -  **VPC**: Use the default value. If there is no available VPC, click **View VPC** to access the VPC console and create a new VPC.
   -  **Subnet**: Use the default value.
   -  **Security Group**: Select **Auto create**.
   -  **EIP**: Select **Bind later**.
   -  **Enterprise Project**: Use the default value.
   -  **Instance Specifications**: Select General Computing S3 -> 8 vCPUs \| 16 GB (s3.2xlarge.2) for both Master and Core nodes.
   -  **System Disk**: Select **Common I/O** and retain the default settings.
   -  **Data Disk**: Select **Common I/O** and retain the default settings.
   -  **Instance Count**: The default number of Master nodes is 2, and that of Core nodes is 3.

#. Click **Next**. The **Set Advanced Options** tab page is displayed. Configure the following parameters. Retain the default settings for the other parameters.

   -  Kerberos authentication:

      -  **Kerberos Authentication**: Disable Kerberos authentication.
      -  **Username**: name of the Manager administrator. **admin** is used by default.
      -  **Password**: password of the Manager administrator.

   -  **Login Mode**: Select a mode for logging in to an ECS.

      -  **Password**: Set a password for logging in to an ECS.
      -  **Key Pair**: Select a key pair from the drop-down list. Select **"I acknowledge that I have obtained private key file** *SSHkey-xxx* **and that without this file I will not be able to log in to my ECS.**" If you have never created a key pair, click **View Key Pair** to create or import a key pair. And then, obtain a private key file.

   -  **Secure Communications**: Select **Enable**.

#. Click **Apply Now**.

   If Kerberos authentication is enabled for a cluster, check whether Kerberos authentication is required. If yes, click **Continue**. If no, click **Back** to disable Kerberos authentication and then create a cluster.

#. Click **Back to Cluster List** to view the cluster status.

   It takes some time to create a cluster. The initial status of the cluster is **Starting**. After the cluster has been created successfully, the cluster status becomes **Running**.
