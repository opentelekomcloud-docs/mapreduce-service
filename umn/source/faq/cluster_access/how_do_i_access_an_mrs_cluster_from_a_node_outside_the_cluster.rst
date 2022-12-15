:original_name: mrs_03_1234.html

.. _mrs_03_1234:

How Do I Access an MRS Cluster from a Node Outside the Cluster?
===============================================================

Creating a Linux ECS Outside the Cluster to Access the MRS Cluster
------------------------------------------------------------------

#. Create an ECS outside the cluster.

   Set **AZ**, **VPC**, and **Security Group** of the ECS to the same values as those of the cluster to be accessed.

2. On the VPC management console, apply for an EIP and bind it to the ECS.
3. Configure security group rules for the cluster.

   a. On the **Dashboard** tab page, click **Add Security Group Rule**. In the **Add Security Group Rule** dialog box that is displayed, click **Manage Security Group Rule**.

   b. Click the **Inbound Rules** tab, and click **Add Rule**. In the **Add Inbound Rule** dialog box, configure the IP address of the ECS and enable all ports.

   c. After the security group rule is added, you can download and install the client on the ECS..

   d. Use the client.

      Log in to the client node as the client installation user and run the following command to switch to the client directory:

      **cd /opt/hadoopclient**

      Run the following command to load environment variables:

      **source bigdata_env**

      If Kerberos authentication is enabled for the cluster, run the following command to authenticate the user. If Kerberos authentication is disabled for the current cluster, authentication is not required.

      **kinit** *MRS cluster user*

      Example:

      **kinit admin**

      Run the client command of a component.

      Example:

      Run the following command to view files in the HDFS root directory:

      **hdfs dfs -ls /**

      .. code-block::

         Found 15 items
         drwxrwx--x   - hive       hive                0 2021-10-26 16:30 /apps
         drwxr-xr-x   - hdfs       hadoop              0 2021-10-18 20:54 /datasets
         drwxr-xr-x   - hdfs       hadoop              0 2021-10-18 20:54 /datastore
         drwxrwx---+  - flink      hadoop              0 2021-10-18 21:10 /flink
         drwxr-x---   - flume      hadoop              0 2021-10-18 20:54 /flume
         drwxrwx--x   - hbase      hadoop              0 2021-10-30 07:31 /hbase
         ...
