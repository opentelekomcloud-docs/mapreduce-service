:original_name: mrs_02_0028.html

.. _mrs_02_0028:

Creating a Cluster and Running a Job
====================================

Function
--------

This API is used to create an MRS cluster and submit a job in the cluster. This API is incompatible with Sahara.

A maximum of 10 clusters can be concurrently created.

Before using the API, you need to obtain the resources listed in :ref:`Table 1 <mrs_02_0028__tbbd2986d18874f82a8ab886ac25a57f8>`.

.. _mrs_02_0028__tbbd2986d18874f82a8ab886ac25a57f8:

.. table:: **Table 1** Obtaining resources

   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Resource                          | How to Obtain                                                                                                                                                                                    |
   +===================================+==================================================================================================================================================================================================+
   | VPC                               | See operation instructions in **VPC > Querying VPCs** and **VPC > Creating a VPC** in the *VPC API Reference*.                                                                                   |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Subnet                            | See operation instructions in **Subnet > Querying Subnets** and **Subnet > Creating a Subnet** in the *VPC API Reference*.                                                                       |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key Pair                          | See operation instructions in **ECS SSH Key Management > Querying SSH Key Pairs** and **ECS SSH Key Management > Creating and Importing an SSH Key Pair** in the *ECS API Reference*.            |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Region                            | Obtain the region and AZ information. For more information about regions and AZs, see `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__.                      |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Version                           | Currently, the following versions are supported: MRS 3.1.2-LTS.6 and MRS 3.2.0-LTS.2.                                                                                                            |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Component                         | -  MRS 3.2.0-LTS.2 supports the following components:                                                                                                                                            |
   |                                   |                                                                                                                                                                                                  |
   |                                   |    -  An analysis cluster contains the following components: Hadoop, Spark2x, HBase, Hive, Hue, Loader, Flink, Oozie, ZooKeeper, HetuEngine, Ranger, and Tez.                                    |
   |                                   |    -  A streaming cluster contains the following components: Kafka, Flume, ZooKeeper, and Ranger.                                                                                                |
   |                                   |    -  A hybrid cluster contains the following components: Hadoop, Spark2x, HBase, Hive, Hue, Loader, Flink, Oozie, ZooKeeper, HetuEngine, Ranger, Tez, Kafka, and Flume.                         |
   |                                   |                                                                                                                                                                                                  |
   |                                   |    -  A custom cluster contains the following components: CDL, Hadoop, Spark2x, HBase, Hive, Hue, Loader, IoTDB, Kafka, Flume, Flink, Oozie, ZooKeeper, HetuEngine, Ranger, Tez, and ClickHouse. |
   |                                   |                                                                                                                                                                                                  |
   |                                   | -  MRS 3.1.2-LTS.6 supports the following components:                                                                                                                                            |
   |                                   |                                                                                                                                                                                                  |
   |                                   |    -  The analysis cluster contains the following components: Hadoop, Spark2x, HBase, Hive, Hue, HetuEngine, Loader, Flink, Oozie, ZooKeeper, Ranger, and Tez.                                   |
   |                                   |    -  The streaming cluster contains the following components: Kafka, Flume, ZooKeeper, and Ranger.                                                                                              |
   |                                   |    -  The hybrid cluster contains the following components: Hadoop, Spark2x, HBase, Hive, Hue, HetuEngine, Loader, Flink, Oozie, ZooKeeper, Ranger, Tez, Kafka, and Flume.                       |
   |                                   |    -  A custom cluster contains the following components: Hadoop, Spark2x, HBase, Hive, Hue, HetuEngine, Loader, Kafka, Flume, Flink, Oozie, ZooKeeper, Ranger, Tez, and ClickHouse.             |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

URI
---

-  Format

   POST /v1.1/{project_id}/run-job-flow

-  Parameter description

   .. table:: **Table 2** URI parameter description

      +------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | Parameter  | Mandatory | Description                                                                                               |
      +============+===========+===========================================================================================================+
      | project_id | Yes       | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
      +------------+-----------+-----------------------------------------------------------------------------------------------------------+

Request
-------

.. table:: **Table 3** Request parameter description

   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                                                                                                              |
   +=======================+=================+=================+==========================================================================================================================================================================================================================================================================================================================================================================+
   | billing_type          | Yes             | Integer         | Cluster billing mode. Set this parameter to **12**.                                                                                                                                                                                                                                                                                                                      |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | data_center           | Yes             | String          | Region of the cluster. For details, see `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__.                                                                                                                                                                                                                                            |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | available_zone_id     | Yes             | String          | AZ ID. For details, see `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__.                                                                                                                                                                                                                                                            |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | -  Region: eu-de                                                                                                                                                                                                                                                                                                                                                         |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 |    -  AZ1(eu-de-01): eu-de-01                                                                                                                                                                                                                                                                                                                                            |
   |                       |                 |                 |    -  AZ2(eu-de-02): eu-de-02                                                                                                                                                                                                                                                                                                                                            |
   |                       |                 |                 |    -  AZ3(eu-de-03): eu-de-03                                                                                                                                                                                                                                                                                                                                            |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | -  Region: eu-nl                                                                                                                                                                                                                                                                                                                                                         |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 |    -  AZ1(eu-nl-01): eu-nl-01                                                                                                                                                                                                                                                                                                                                            |
   |                       |                 |                 |    -  AZ2(eu-nl-02): eu-nl-02                                                                                                                                                                                                                                                                                                                                            |
   |                       |                 |                 |    -  AZ3(eu-nl-03): eu-nl-03                                                                                                                                                                                                                                                                                                                                            |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | cluster_name          | Yes             | String          | Cluster name. It must be unique.                                                                                                                                                                                                                                                                                                                                         |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | It contains only 1 to 64 characters. Only letters, digits, hyphens (-), and underscores (_) are allowed.                                                                                                                                                                                                                                                                 |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | vpc                   | Yes             | String          | Name of the VPC where the subnet locates                                                                                                                                                                                                                                                                                                                                 |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | Perform the following operations to obtain the VPC name from the VPC management console:                                                                                                                                                                                                                                                                                 |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | #. Log in to the management console.                                                                                                                                                                                                                                                                                                                                     |
   |                       |                 |                 | #. Click **Virtual Private Cloud** and select **Virtual Private Cloud** from the left list.                                                                                                                                                                                                                                                                              |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | On the **Virtual Private Cloud** page, obtain the VPC name from the list.                                                                                                                                                                                                                                                                                                |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | vpc_id                | Yes             | String          | ID of the VPC where the subnet locates                                                                                                                                                                                                                                                                                                                                   |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | Perform the following operations to obtain the VPC ID from the VPC management console:                                                                                                                                                                                                                                                                                   |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | #. Log in to the management console.                                                                                                                                                                                                                                                                                                                                     |
   |                       |                 |                 | #. Click **Virtual Private Cloud** and select **Virtual Private Cloud** from the left list.                                                                                                                                                                                                                                                                              |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | On the **Virtual Private Cloud** page, obtain the VPC ID from the list.                                                                                                                                                                                                                                                                                                  |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | subnet_id             | Yes             | String          | Network ID                                                                                                                                                                                                                                                                                                                                                               |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | Perform the following operations to obtain the network ID of the VPC from the VPC management console:                                                                                                                                                                                                                                                                    |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | #. Log in to the management console.                                                                                                                                                                                                                                                                                                                                     |
   |                       |                 |                 | #. Click **Virtual Private Cloud** and select **Virtual Private Cloud** from the left list.                                                                                                                                                                                                                                                                              |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | On the **Virtual Private Cloud** page, obtain the network ID of the VPC from the list.                                                                                                                                                                                                                                                                                   |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | subnet_name           | Yes             | String          | Subnet name                                                                                                                                                                                                                                                                                                                                                              |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | Perform the following operations to obtain the subnet name from the VPC management console:                                                                                                                                                                                                                                                                              |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | #. Log in to the management console.                                                                                                                                                                                                                                                                                                                                     |
   |                       |                 |                 | #. Click **Virtual Private Cloud** and select **Virtual Private Cloud** from the left list.                                                                                                                                                                                                                                                                              |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | On the **Virtual Private Cloud** page, obtain the subnet name of the VPC from the list.                                                                                                                                                                                                                                                                                  |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | security_groups_id    | No              | String          | Security group ID of the cluster                                                                                                                                                                                                                                                                                                                                         |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | -  If this parameter is left blank, MRS automatically creates a security group, whose name starts with **mrs_{cluster_name}**.                                                                                                                                                                                                                                           |
   |                       |                 |                 | -  If this parameter is not left blank, a fixed security group is used to create a cluster. The transferred ID must be the security group ID owned by the current tenant. The security group must include an inbound rule in which all protocols and all ports are allowed and the source is the IP address of the specified node on the management plane.               |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | tags                  | No              | Array           | Cluster tag                                                                                                                                                                                                                                                                                                                                                              |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | -  A cluster allows a maximum of 10 tags. A tag name (key) must be unique in a cluster.                                                                                                                                                                                                                                                                                  |
   |                       |                 |                 | -  A tag key or value cannot contain the following special characters: ``=*<>\,|/``                                                                                                                                                                                                                                                                                      |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | cluster_version       | Yes             | String          | Cluster version                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | Possible values are as follows:                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | -  MRS 3.1.2-LTS.6                                                                                                                                                                                                                                                                                                                                                       |
   |                       |                 |                 | -  MRS 3.2.0-LTS.2                                                                                                                                                                                                                                                                                                                                                       |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | cluster_type          | No              | Integer         | Cluster type                                                                                                                                                                                                                                                                                                                                                             |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | -  **0**: analysis cluster                                                                                                                                                                                                                                                                                                                                               |
   |                       |                 |                 | -  **1**: streaming cluster                                                                                                                                                                                                                                                                                                                                              |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | The default value is **0**.                                                                                                                                                                                                                                                                                                                                              |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | Note: Currently, hybrid clusters cannot be created using APIs.                                                                                                                                                                                                                                                                                                           |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | safe_mode             | Yes             | Integer         | Running mode of an MRS cluster                                                                                                                                                                                                                                                                                                                                           |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | -  **0**: normal cluster. In a normal cluster, Kerberos authentication is disabled, and users can use all functions provided by the cluster.                                                                                                                                                                                                                             |
   |                       |                 |                 | -  **1**: security cluster. In a security cluster, Kerberos authentication is enabled, and common users cannot use the file management and job management functions of an MRS cluster or view cluster resource usage and the job records of Hadoop and Spark. To use these functions, the users must obtain the relevant permissions from the MRS Manager administrator. |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | cluster_admin_secret  | Yes             | String          | Password of the MRS Manager administrator                                                                                                                                                                                                                                                                                                                                |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | -  Must contain 8 to 32 characters.                                                                                                                                                                                                                                                                                                                                      |
   |                       |                 |                 | -  Must contain at least three of the following:                                                                                                                                                                                                                                                                                                                         |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 |    -  Lowercase letters                                                                                                                                                                                                                                                                                                                                                  |
   |                       |                 |                 |    -  Uppercase letters                                                                                                                                                                                                                                                                                                                                                  |
   |                       |                 |                 |    -  Digits                                                                                                                                                                                                                                                                                                                                                             |
   |                       |                 |                 |    -  Special characters: :literal:`\`~!@#$%^&*()-_=+\\|[{}];:'",<.>/?` and space                                                                                                                                                                                                                                                                                        |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | -  Cannot be the username or the username spelled backwards.                                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | login_mode            | Yes             | Integer         | Cluster login mode                                                                                                                                                                                                                                                                                                                                                       |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | -  **0**: password                                                                                                                                                                                                                                                                                                                                                       |
   |                       |                 |                 | -  **1**: key pair                                                                                                                                                                                                                                                                                                                                                       |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | The default value is **1**.                                                                                                                                                                                                                                                                                                                                              |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | -  If **login_mode** is set to **0**, the request body contains the **cluster_master_secret** field.                                                                                                                                                                                                                                                                     |
   |                       |                 |                 | -  If **login_mode** is set to **1**, the request body contains the **node_public_cert_name** field.                                                                                                                                                                                                                                                                     |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | cluster_master_secret | No              | String          | Password of user **root** for logging in to a cluster node                                                                                                                                                                                                                                                                                                               |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | If **login_mode** is set to **0**, the request body contains the **cluster_master_secret** field.                                                                                                                                                                                                                                                                        |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | A password must meet the following requirements:                                                                                                                                                                                                                                                                                                                         |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | -  Must be 8 to 26 characters long.                                                                                                                                                                                                                                                                                                                                      |
   |                       |                 |                 | -  Must contain at least three of the following: uppercase letters, lowercase letters, digits, and special characters (``!@$%^-_=+[{}]:,./?``), but must not contain spaces.                                                                                                                                                                                             |
   |                       |                 |                 | -  Cannot be the username or the username spelled backwards.                                                                                                                                                                                                                                                                                                             |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | node_public_cert_name | No              | String          | Name of a key pair You can use a key pair to log in to the Master node in the cluster.                                                                                                                                                                                                                                                                                   |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | If **login_mode** is set to **1**, the request body contains                                                                                                                                                                                                                                                                                                             |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | the **node_public_cert_name** field.                                                                                                                                                                                                                                                                                                                                     |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | log_collection        | No              | Integer         | Whether to collect logs when cluster creation fails                                                                                                                                                                                                                                                                                                                      |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | -  **0**: Do not collect.                                                                                                                                                                                                                                                                                                                                                |
   |                       |                 |                 | -  **1**: Collect.                                                                                                                                                                                                                                                                                                                                                       |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | The default value is **1**, indicating that OBS buckets will be created and only used to collect logs that record MRS cluster creation failures.                                                                                                                                                                                                                         |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | node_groups           | No              | Array           | List of nodes. For more parameter description, see :ref:`Table 4 <mrs_02_0028__table3419221413>`.                                                                                                                                                                                                                                                                        |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 | .. note::                                                                                                                                                                                                                                                                                                                                                                |
   |                       |                 |                 |                                                                                                                                                                                                                                                                                                                                                                          |
   |                       |                 |                 |    You can select either this parameter or the parameter listed in :ref:`Table 5 <mrs_02_0028__table1231363418103>`.                                                                                                                                                                                                                                                     |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | component_list        | Yes             | Array           | List of service components to be installed. For more parameter description, see :ref:`Table 7 <mrs_02_0028__te1288dba79844d3fa5973939a3739d34>`.                                                                                                                                                                                                                         |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | add_jobs              | No              | Array           | Jobs can be submitted when a cluster is created. Currently, only one job can be created. For details about job parameters, see :ref:`Table 8 <mrs_02_0028__t8ded0b3ae11742cea98a467ce26fd093>`.                                                                                                                                                                          |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | bootstrap_scripts     | No              | Array           | Bootstrap action script information. For more parameter description, see :ref:`Table 15 <mrs_02_0028__table1258382865010>`.                                                                                                                                                                                                                                              |
   +-----------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0028__table3419221413:

.. table:: **Table 4** **node_groups** parameter description

   +---------------------+-----------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter           | Mandatory       | Type              | Description                                                                                                                                                                                                                 |
   +=====================+=================+===================+=============================================================================================================================================================================================================================+
   | group_name          | Yes             | String            | Node group name.                                                                                                                                                                                                            |
   |                     |                 |                   |                                                                                                                                                                                                                             |
   |                     |                 |                   | -  master_node_default_group                                                                                                                                                                                                |
   |                     |                 |                   | -  core_node_analysis_group                                                                                                                                                                                                 |
   |                     |                 |                   | -  core_node_streaming_group                                                                                                                                                                                                |
   |                     |                 |                   | -  task_node_analysis_group                                                                                                                                                                                                 |
   |                     |                 |                   | -  task_node_streaming_group                                                                                                                                                                                                |
   +---------------------+-----------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | node_num            | Yes             | Integer           | Number of nodes. The value ranges from 0 to 500 and the default value is **0**. The total number of Core and Task nodes cannot exceed 500.                                                                                  |
   +---------------------+-----------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | node_size           | Yes             | String            | Instance specifications of a node. For details about the configuration method, see the remarks of **master_node_size**.                                                                                                     |
   +---------------------+-----------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | root_volume_size    | Yes             | String            | Data disk storage space of a node.                                                                                                                                                                                          |
   +---------------------+-----------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | root_volume_type    | Yes             | String            | Data disk storage type of a node. Currently, SATA, SAS and SSD are supported.                                                                                                                                               |
   |                     |                 |                   |                                                                                                                                                                                                                             |
   |                     |                 |                   | -  SATA: Common I/O                                                                                                                                                                                                         |
   |                     |                 |                   | -  SAS: High I/O                                                                                                                                                                                                            |
   |                     |                 |                   | -  SSD: Ultra-high I/O                                                                                                                                                                                                      |
   +---------------------+-----------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | data_volume_type    | Yes             | String            | Data disk storage type of a node. Currently, SATA, SAS and SSD are supported.                                                                                                                                               |
   |                     |                 |                   |                                                                                                                                                                                                                             |
   |                     |                 |                   | -  SATA: Common I/O                                                                                                                                                                                                         |
   |                     |                 |                   | -  SAS: High I/O                                                                                                                                                                                                            |
   |                     |                 |                   | -  SSD: Ultra-high I/O                                                                                                                                                                                                      |
   +---------------------+-----------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | data_volume_count   | Yes             | Integer           | Number of data disks of a node.                                                                                                                                                                                             |
   |                     |                 |                   |                                                                                                                                                                                                                             |
   |                     |                 |                   | Value range: 0 to 10                                                                                                                                                                                                        |
   +---------------------+-----------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | data_volume_size    | Yes             | Integer           | Data disk storage space of a node.                                                                                                                                                                                          |
   |                     |                 |                   |                                                                                                                                                                                                                             |
   |                     |                 |                   | Value range: 100 GB to 32,000 GB                                                                                                                                                                                            |
   +---------------------+-----------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | auto_scaling_policy | No              | AutoScalingPolicy | Auto scaling rule information. This parameter is valid only when **group_name** is set to **task_node_analysis_group** or **task_node_streaming_group**. For details, see :ref:`Table 5 <mrs_02_0028__table1231363418103>`. |
   +---------------------+-----------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0028__table1231363418103:

.. table:: **Table 5** Node configuration parameters

   +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                                                                                                                                                                      |
   +==========================+=================+=================+==================================================================================================================================================================================================================================================================================================================================================================================================================================+
   | master_node_num          | Yes             | Integer         | Number of Master nodes. If cluster HA is enabled, set this parameter to **2**. If cluster HA is disabled, set this parameter to **1**.                                                                                                                                                                                                                                                                                           |
   +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | master_node_size         | Yes             | String          | Instance specifications of the Master node, for example, **c6.4xlarge.4linux.mrs**. MRS supports host specifications determined by CPU, memory, and disk space. For details about instance specifications, see :ref:`ECS Specifications Used by MRS <mrs_01_9005>`.                                                                                                                                                              |
   +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | core_node_num            | Yes             | Integer         | Number of Core nodes                                                                                                                                                                                                                                                                                                                                                                                                             |
   |                          |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                          |                 |                 | Value range: 1 to 500                                                                                                                                                                                                                                                                                                                                                                                                            |
   |                          |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                          |                 |                 | A maximum of 500 Core nodes are supported by default. If more than 500 Core nodes are required, contact technical support.                                                                                                                                                                                                                                                                                                       |
   +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | core_node_size           | Yes             | String          | Instance specifications of the Core node, for example, **c6.4xlarge.4linux.mrs**.                                                                                                                                                                                                                                                                                                                                                |
   +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | master_data_volume_type  | No              | String          | This parameter is a multi-disk parameter, indicating the data disk storage type of the Master node. Currently, SATA, SAS and SSD are supported.                                                                                                                                                                                                                                                                                  |
   +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | master_data_volume_size  | No              | Integer         | This parameter is a multi-disk parameter, indicating the data disk storage space of the Master node. To increase data storage capacity, you can add disks at the same time when creating a cluster.                                                                                                                                                                                                                              |
   |                          |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                          |                 |                 | Value range: 100 GB to 32,000 GB                                                                                                                                                                                                                                                                                                                                                                                                 |
   +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | master_data_volume_count | No              | Integer         | This parameter is a multi-disk parameter, indicating the number of data disks of the Master node.                                                                                                                                                                                                                                                                                                                                |
   |                          |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                          |                 |                 | The value can be set to **1** only.                                                                                                                                                                                                                                                                                                                                                                                              |
   +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | core_data_volume_type    | No              | String          | This parameter is a multi-disk parameter, indicating the data disk storage type of the Core node. Currently, SATA, SAS and SSD are supported.                                                                                                                                                                                                                                                                                    |
   +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | core_data_volume_size    | No              | Integer         | This parameter is a multi-disk parameter, indicating the data disk storage space of the Core node. To increase data storage capacity, you can add disks at the same time when creating a cluster.                                                                                                                                                                                                                                |
   |                          |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                          |                 |                 | Value range: 100 GB to 32,000 GB                                                                                                                                                                                                                                                                                                                                                                                                 |
   +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | core_data_volume_count   | No              | Integer         | This parameter is a multi-disk parameter, indicating the number of data disks of the Core node.                                                                                                                                                                                                                                                                                                                                  |
   |                          |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                          |                 |                 | Value range: 1 to 10                                                                                                                                                                                                                                                                                                                                                                                                             |
   +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | volume_type              | No              | String          | Data disk storage type of the Master and Core nodes. Currently, SATA, SAS and SSD are supported. Disk parameters can be represented by **volume_type** and **volume_size**, or multi-disk parameters. If the **volume_type** and **volume_size** parameters coexist with the multi-disk parameters, the system reads the **volume_type** and **volume_size** parameters first. You are advised to use the multi-disk parameters. |
   |                          |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                          |                 |                 | -  SATA: Common I/O                                                                                                                                                                                                                                                                                                                                                                                                              |
   |                          |                 |                 | -  SAS: High I/O                                                                                                                                                                                                                                                                                                                                                                                                                 |
   |                          |                 |                 | -  SSD: Ultra-high I/O                                                                                                                                                                                                                                                                                                                                                                                                           |
   +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | volume_size              | No              | Integer         | Data disk storage space of the Master and Core nodes. To increase data storage capacity, you can add disks at the same time when creating a cluster. Select a proper disk storage space based on the following application scenarios:                                                                                                                                                                                            |
   |                          |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                          |                 |                 | -  Separation of data storage and computing: Data is stored in the OBS system. Costs of clusters are relatively low but computing performance is poor. The clusters can be deleted at any time. It is recommended when data computing is infrequently performed.                                                                                                                                                                 |
   |                          |                 |                 | -  Integration of data storage and computing: Data is stored in the HDFS system. Costs of clusters are relatively high but computing performance is good. The clusters cannot be deleted in a short term. It is recommended when data computing is frequently performed.                                                                                                                                                         |
   |                          |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                          |                 |                 | Value range: 100 GB to 32,000 GB                                                                                                                                                                                                                                                                                                                                                                                                 |
   |                          |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                          |                 |                 | This parameter is not recommended. For details, see the description of the **volume_type** parameter.                                                                                                                                                                                                                                                                                                                            |
   +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | task_node_groups         | No              | Array           | List of Task nodes For more parameter description, see :ref:`Table 6 <mrs_02_0028__tc6bfa2a3d7a348d786a901f3a9327b50>`.                                                                                                                                                                                                                                                                                                          |
   +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0028__tc6bfa2a3d7a348d786a901f3a9327b50:

.. table:: **Table 6** **task_node_groups** parameter description

   +---------------------+-----------------+-------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter           | Mandatory       | Type              | Description                                                                                                                                                                           |
   +=====================+=================+===================+=======================================================================================================================================================================================+
   | node_num            | Yes             | Integer           | Number of Task nodes. The value ranges from 0 to 500 and the total number of Core and Task nodes cannot exceed 500.                                                                   |
   +---------------------+-----------------+-------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | node_size           | Yes             | String            | Instance specifications of the Task node, for example, **c6.4xlarge.4linux.mrs**. For details about instance specifications, see :ref:`ECS Specifications Used by MRS <mrs_01_9005>`. |
   +---------------------+-----------------+-------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | data_volume_type    | Yes             | String            | Data disk storage type of the Task node, supporting SATA, SAS, and SSD currently                                                                                                      |
   |                     |                 |                   |                                                                                                                                                                                       |
   |                     |                 |                   | -  SATA: Common I/O                                                                                                                                                                   |
   |                     |                 |                   | -  SAS: High I/O                                                                                                                                                                      |
   |                     |                 |                   | -  SSD: Ultra-high I/O                                                                                                                                                                |
   +---------------------+-----------------+-------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | data_volume_count   | Yes             | Integer           | Number of data disks of a Task node                                                                                                                                                   |
   |                     |                 |                   |                                                                                                                                                                                       |
   |                     |                 |                   | Value range: 0 to 10                                                                                                                                                                  |
   +---------------------+-----------------+-------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | data_volume_size    | Yes             | Integer           | Data disk storage space of a Task node                                                                                                                                                |
   |                     |                 |                   |                                                                                                                                                                                       |
   |                     |                 |                   | Value range: 100 GB to 32,000 GB                                                                                                                                                      |
   +---------------------+-----------------+-------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | auto_scaling_policy | No              | AutoScalingPolicy | Auto scaling policy. For details, see :ref:`Table 9 <mrs_02_0028__t6d6054a35d6342dc9dc5b3b8580fec7c>`.                                                                                |
   +---------------------+-----------------+-------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0028__te1288dba79844d3fa5973939a3739d34:

.. table:: **Table 7** **component_list** parameter description

   ============== ========= ====== ==============
   Parameter      Mandatory Type   Description
   ============== ========= ====== ==============
   component_name Yes       String Component name
   ============== ========= ====== ==============

.. _mrs_02_0028__t8ded0b3ae11742cea98a467ce26fd093:

.. table:: **Table 8** **add_jobs** parameter description

   +-----------------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                   | Mandatory       | Type            | Description                                                                                                                                               |
   +=============================+=================+=================+===========================================================================================================================================================+
   | job_type                    | Yes             | Integer         | Job type code                                                                                                                                             |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | -  1: MapReduce                                                                                                                                           |
   |                             |                 |                 | -  2: Spark                                                                                                                                               |
   |                             |                 |                 | -  3: Hive Script                                                                                                                                         |
   |                             |                 |                 | -  4: HiveQL (not supported currently)                                                                                                                    |
   |                             |                 |                 | -  5: DistCp, importing and exporting data (not supported currently)                                                                                      |
   |                             |                 |                 | -  6: Spark Script                                                                                                                                        |
   |                             |                 |                 | -  7: Spark SQL, submitting Spark SQL statements (not supported currently).                                                                               |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 |    .. note::                                                                                                                                              |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 |       Spark and Hive jobs can be added to only clusters that include Spark and Hive components.                                                           |
   +-----------------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_name                    | Yes             | String          | Job name. It contains 1 to 64 characters. Only letters, digits, hyphens (-), and underscores (_) are allowed.                                             |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | .. note::                                                                                                                                                 |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 |    Identical job names are allowed but not recommended.                                                                                                   |
   +-----------------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | jar_path                    | No              | String          | Path of the JAR or SQL file for program execution. The parameter must meet the following requirements:                                                    |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | -  Contains a maximum of 1,023 characters, excluding special characters such as ``;|&><'$.`` The parameter value cannot be empty or full of spaces.       |
   |                             |                 |                 | -  Files can be stored in HDFS or OBS. The path varies depending on the file system.                                                                      |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 |    -  OBS: The path must start with **s3a://**. Files or programs encrypted by KMS are not supported.                                                     |
   |                             |                 |                 |    -  HDFS: The path starts with a slash (**/**).                                                                                                         |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | -  Spark Script must end with **.sql** while MapReduce and Spark Jar must end with **.jar**. **sql** and **jar** are case-insensitive.                    |
   +-----------------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | arguments                   | No              | String          | Key parameter for program execution. The parameter is specified by the function of the user's program. MRS is only responsible for loading the parameter. |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | The parameter contains a maximum of 2,047 characters, excluding special characters such as ``;|&>'<$,`` and can be left blank.                            |
   +-----------------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | input                       | No              | String          | Address for inputting data.                                                                                                                               |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | Files can be stored in HDFS or OBS. The path varies depending on the file system.                                                                         |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | -  OBS: The path must start with **s3a://**. Files or programs encrypted by KMS are not supported.                                                        |
   |                             |                 |                 | -  HDFS: The path starts with a slash (**/**).                                                                                                            |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | The parameter contains a maximum of 1,023 characters, excluding special characters such as ``;|&>'<$,`` and can be left blank.                            |
   +-----------------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | output                      | No              | String          | Address for outputting data.                                                                                                                              |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | Files can be stored in HDFS or OBS. The path varies depending on the file system.                                                                         |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | -  OBS: The path must start with **s3a://**.                                                                                                              |
   |                             |                 |                 | -  HDFS: The path starts with a slash (**/**).                                                                                                            |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | If the specified path does not exist, the system will automatically create it.                                                                            |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | The parameter contains a maximum of 1,023 characters, excluding special characters such as ``;|&>'<$,`` and can be left blank.                            |
   +-----------------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_log                     | No              | String          | Path for storing job logs that record job running status.                                                                                                 |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | Files can be stored in HDFS or OBS. The path varies depending on the file system.                                                                         |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | -  OBS: The path must start with **s3a://**.                                                                                                              |
   |                             |                 |                 | -  HDFS: The path starts with a slash (**/**).                                                                                                            |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | The parameter contains a maximum of 1,023 characters, excluding special characters such as ``;|&>'<$,`` and can be left blank.                            |
   +-----------------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | shutdown_cluster            | No              | Bool            | Whether to delete the cluster after the job execution is complete                                                                                         |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | -  **true**: Yes                                                                                                                                          |
   |                             |                 |                 | -  **false**: No                                                                                                                                          |
   +-----------------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | file_action                 | No              | String          | Data import and export                                                                                                                                    |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | -  **import**                                                                                                                                             |
   |                             |                 |                 | -  **export**                                                                                                                                             |
   +-----------------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | submit_job_once_cluster_run | Yes             | Bool            | -  **true**: Submit a job during cluster creation.                                                                                                        |
   |                             |                 |                 | -  **false**: Submit a job after the cluster is created.                                                                                                  |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | Set this parameter to **true** in this example.                                                                                                           |
   +-----------------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hql                         | No              | String          | HiveQL statement                                                                                                                                          |
   +-----------------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hive_script_path            | Yes             | String          | SQL program path. This parameter is needed by Spark Script and Hive Script jobs only, and must meet the following requirements:                           |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | -  Contains a maximum of 1,023 characters, excluding special characters such as ``;|&><'$.`` The parameter value cannot be empty or full of spaces.       |
   |                             |                 |                 | -  Files can be stored in HDFS or OBS. The path varies depending on the file system.                                                                      |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 |    -  OBS: The path must start with **s3a://**. Files or programs encrypted by KMS are not supported.                                                     |
   |                             |                 |                 |    -  HDFS: The path starts with a slash (**/**).                                                                                                         |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | -  Ends with **.sql**. **sql** is case-insensitive.                                                                                                       |
   +-----------------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0028__t6d6054a35d6342dc9dc5b3b8580fec7c:

.. table:: **Table 9** **auto_scaling_policy** parameter description

   +---------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter           | Mandatory       | Type            | Description                                                                                                                                                                |
   +=====================+=================+=================+============================================================================================================================================================================+
   | auto_scaling_enable | Yes             | Boolean         | Whether to enable the auto scaling rule.                                                                                                                                   |
   +---------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | min_capacity        | Yes             | Integer         | Minimum number of nodes left in the node group.                                                                                                                            |
   |                     |                 |                 |                                                                                                                                                                            |
   |                     |                 |                 | Value range: 0 to 500                                                                                                                                                      |
   +---------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | max_capacity        | Yes             | Integer         | Maximum number of nodes in the node group.                                                                                                                                 |
   |                     |                 |                 |                                                                                                                                                                            |
   |                     |                 |                 | Value range: 0 to 500                                                                                                                                                      |
   +---------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resources_plans     | No              | List            | Resource plan list. For details, see :ref:`Table 10 <mrs_02_0028__table10281451162111>`. If this parameter is left blank, the resource plan is disabled.                   |
   |                     |                 |                 |                                                                                                                                                                            |
   |                     |                 |                 | When auto scaling is enabled, either a resource plan or an auto scaling rule must be configured.                                                                           |
   +---------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | exec_scripts        | No              | List            | List of custom scaling automation scripts. For details, see :ref:`Table 11 <mrs_02_0028__table1921110172216>`. If this parameter is left blank, a hook script is disabled. |
   +---------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | rules               | No              | List            | List of auto scaling rules. For details, see :ref:`Table 12 <mrs_02_0028__t4c9e3e169631470d81d260543affb7e1>`.                                                             |
   |                     |                 |                 |                                                                                                                                                                            |
   |                     |                 |                 | When auto scaling is enabled, either a resource plan or an auto scaling rule must be configured.                                                                           |
   +---------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0028__table10281451162111:

.. table:: **Table 10** **resources_plan** parameter description

   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                               |
   +=================+=================+=================+===========================================================================================================================================================================================+
   | period_type     | Yes             | String          | Cycle type of a resource plan. Currently, only the following cycle type is supported:                                                                                                     |
   |                 |                 |                 |                                                                                                                                                                                           |
   |                 |                 |                 | -  **daily**                                                                                                                                                                              |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | start_time      | Yes             | String          | Start time of a resource plan. The value is in the format of **hour:minute**, indicating that the time ranges from 0:00 to 23:59.                                                         |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | end_time        | Yes             | String          | End time of a resource plan. The value is in the same format as that of **start_time**. The interval between **end_time** and **start_time** must be greater than or equal to 30 minutes. |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | min_capacity    | Yes             | Integer         | Minimum number of the preserved nodes in a node group in a resource plan.                                                                                                                 |
   |                 |                 |                 |                                                                                                                                                                                           |
   |                 |                 |                 | Value range: 0 to 500                                                                                                                                                                     |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | max_capacity    | Yes             | Integer         | Maximum number of the preserved nodes in a node group in a resource plan.                                                                                                                 |
   |                 |                 |                 |                                                                                                                                                                                           |
   |                 |                 |                 | Value range: 0 to 500                                                                                                                                                                     |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0028__table1921110172216:

.. table:: **Table 11** **exec_script** parameter description

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                                     |
   +=================+=================+=================+=================================================================================================================================================================================================================================+
   | name            | Yes             | String          | Name of a custom automation script. It must be unique in a same cluster.                                                                                                                                                        |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | The value can contain only digits, letters, spaces, hyphens (-), and underscores (_) and cannot start with a space.                                                                                                             |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | The value can contain 1 to 64 characters.                                                                                                                                                                                       |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | uri             | Yes             | String          | Path of a custom automation script. Set this parameter to an OBS bucket path or a local VM path.                                                                                                                                |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | -  OBS bucket path: Enter a script path manually, for example, **s3a://**\ *XXX*\ **/scale.sh**.                                                                                                                                |
   |                 |                 |                 | -  Local VM path: Enter a script path. The script path must start with a slash (/) and end with **.sh**.                                                                                                                        |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | parameters      | No              | String          | Parameters of a custom automation script.                                                                                                                                                                                       |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | -  Multiple parameters are separated by space.                                                                                                                                                                                  |
   |                 |                 |                 | -  The following predefined system parameters can be transferred:                                                                                                                                                               |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 |    -  *${mrs_scale_node_num}*: Number of the nodes to be added or removed                                                                                                                                                       |
   |                 |                 |                 |    -  *${mrs_scale_type}*: Scaling type. The value can be **scale_out** or **scale_in**.                                                                                                                                        |
   |                 |                 |                 |    -  *${mrs_scale_node_hostnames}*: Host names of the nodes to be added or removed                                                                                                                                             |
   |                 |                 |                 |    -  *${mrs_scale_node_ips}*: IP addresses of the nodes to be added or removed                                                                                                                                                 |
   |                 |                 |                 |    -  *${mrs_scale_rule_name}*: Name of the rule that triggers auto scaling                                                                                                                                                     |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | -  Other user-defined parameters are used in the same way as those of common shell scripts. Parameters are separated by space.                                                                                                  |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | nodes           | Yes             | List<String>    | Type of a node where the custom automation script is executed. The node type can be Master, Core, or Task.                                                                                                                      |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | active_master   | No              | Boolean         | Whether the custom automation script runs only on the active Master node.                                                                                                                                                       |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | The default value is **false**, indicating that the custom automation script can run on all Master nodes.                                                                                                                       |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | action_stage    | Yes             | String          | Time when a script is executed.                                                                                                                                                                                                 |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | The following four options are supported:                                                                                                                                                                                       |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | -  **before_scale_out**: before scale-out                                                                                                                                                                                       |
   |                 |                 |                 | -  **before_scale_in**: before scale-in                                                                                                                                                                                         |
   |                 |                 |                 | -  **after_scale_out**: after scale-out                                                                                                                                                                                         |
   |                 |                 |                 | -  **after_scale_in**: after scale-in                                                                                                                                                                                           |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | fail_action     | Yes             | String          | Whether to continue to execute subsequent scripts and create a cluster after the custom automation script fails to be executed.                                                                                                 |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | -  **continue**: Continue to execute subsequent scripts.                                                                                                                                                                        |
   |                 |                 |                 | -  **errorout**: Stop the action.                                                                                                                                                                                               |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 |    .. note::                                                                                                                                                                                                                    |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 |       -  You are advised to set this parameter to **continue** in the commissioning phase so that the cluster can continue to be installed and started no matter whether the custom automation script is executed successfully. |
   |                 |                 |                 |       -  The scale-in operation cannot be undone. Therefore, **fail_action** must be set to **continue** for the scripts that are executed after scale-in.                                                                      |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0028__t4c9e3e169631470d81d260543affb7e1:

.. table:: **Table 12** **rules** parameter description

   +--------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+
   | Parameter          | Mandatory       | Type            | Description                                                                                                                    |
   +====================+=================+=================+================================================================================================================================+
   | name               | Yes             | String          | Name of an auto scaling rule.                                                                                                  |
   |                    |                 |                 |                                                                                                                                |
   |                    |                 |                 | It contains only 1 to 64 characters. Only letters, digits, hyphens (-), and underscores (_) are allowed.                       |
   |                    |                 |                 |                                                                                                                                |
   |                    |                 |                 | Rule names must be unique in a node group.                                                                                     |
   +--------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+
   | description        | No              | String          | Description about an auto scaling rule.                                                                                        |
   |                    |                 |                 |                                                                                                                                |
   |                    |                 |                 | It contains a maximum of 1,024 characters.                                                                                     |
   +--------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+
   | adjustment_type    | Yes             | String          | Auto scaling rule adjustment type. The options are as follows:                                                                 |
   |                    |                 |                 |                                                                                                                                |
   |                    |                 |                 | -  **scale_out**: cluster scale-out                                                                                            |
   |                    |                 |                 | -  **scale_in**: cluster scale-in                                                                                              |
   +--------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+
   | cool_down_minutes  | Yes             | Integer         | Cluster cooling time after an auto scaling rule is triggered, when no auto scaling operation is performed. The unit is minute. |
   |                    |                 |                 |                                                                                                                                |
   |                    |                 |                 | Value range: 0 to 10,080. One week is equal to 10,080 minutes.                                                                 |
   +--------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+
   | scaling_adjustment | Yes             | Integer         | Number of nodes that can be adjusted once.                                                                                     |
   |                    |                 |                 |                                                                                                                                |
   |                    |                 |                 | Value range: 1 to 100                                                                                                          |
   +--------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+
   | trigger            | Yes             | Trigger         | Condition for triggering a rule. For details, see :ref:`Table 13 <mrs_02_0028__t03bd10dc0ec94a3babc71b2d5d57c3fe>`.            |
   +--------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0028__t03bd10dc0ec94a3babc71b2d5d57c3fe:

.. table:: **Table 13** **trigger** parameter description

   +---------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter           | Mandatory       | Type            | Description                                                                                                                                                                                                       |
   +=====================+=================+=================+===================================================================================================================================================================================================================+
   | metric_name         | Yes             | String          | Metric name.                                                                                                                                                                                                      |
   |                     |                 |                 |                                                                                                                                                                                                                   |
   |                     |                 |                 | This triggering condition makes a judgment according to the value of the metric.                                                                                                                                  |
   |                     |                 |                 |                                                                                                                                                                                                                   |
   |                     |                 |                 | A metric name contains a maximum of 64 characters.                                                                                                                                                                |
   |                     |                 |                 |                                                                                                                                                                                                                   |
   |                     |                 |                 | :ref:`Table 14 <mrs_02_0028__t27de3279a99a48968dacb015c498d9cb>` lists the supported metric names.                                                                                                                |
   +---------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | metric_value        | Yes             | String          | Metric threshold to trigger a rule                                                                                                                                                                                |
   |                     |                 |                 |                                                                                                                                                                                                                   |
   |                     |                 |                 | The parameter value must be an integer or number with two decimal places only. :ref:`Table 14 <mrs_02_0028__t27de3279a99a48968dacb015c498d9cb>` provides value types and ranges corresponding to **metric_name**. |
   +---------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | comparison_operator | No              | String          | Metric judgment logic operator. The options are as follows:                                                                                                                                                       |
   |                     |                 |                 |                                                                                                                                                                                                                   |
   |                     |                 |                 | -  **LT**: less than                                                                                                                                                                                              |
   |                     |                 |                 | -  **GT**: greater than                                                                                                                                                                                           |
   |                     |                 |                 | -  **LTOE**: less than or equal to                                                                                                                                                                                |
   |                     |                 |                 | -  **GTOE**: greater than or equal to                                                                                                                                                                             |
   +---------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | evaluation_periods  | Yes             | Integer         | Number of consecutive five-minute periods, during which a metric threshold is reached                                                                                                                             |
   |                     |                 |                 |                                                                                                                                                                                                                   |
   |                     |                 |                 | Value range: 1 to 288                                                                                                                                                                                             |
   +---------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0028__t27de3279a99a48968dacb015c498d9cb:

.. table:: **Table 14** Auto scaling metrics

   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   | Cluster Type      | Metric Name                              | Value Type      | Description                                                                                                  |
   +===================+==========================================+=================+==============================================================================================================+
   | Streaming cluster | StormSlotAvailable                       | Integer         | Number of available Storm slots.                                                                             |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSlotAvailablePercentage             | Percentage      | Percentage of available Storm slots, that is, the proportion of the available slots to total slots           |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100                                                                                        |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSlotUsed                            | Integer         | Number of the used Storm slots.                                                                              |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSlotUsedPercentage                  | Percentage      | Percentage of the used Storm slots, that is, the proportion of the used slots to total slots.                |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100                                                                                        |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSupervisorMemAverageUsage           | Integer         | Average memory usage of the Supervisor process of Storm.                                                     |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSupervisorMemAverageUsagePercentage | Percentage      | Average percentage of the used memory of the Supervisor process of Storm to the total memory of the system.  |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100                                                                                        |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSupervisorCPUAverageUsagePercentage | Percentage      | Average percentage of the used CPUs of the Supervisor process of Storm to the total CPUs.                    |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 6,000                                                                                      |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   | Analysis cluster  | YARNAppPending                           | Integer         | Number of pending tasks on Yarn.                                                                             |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNAppPendingRatio                      | Ratio           | Ratio of pending tasks on Yarn, that is, the ratio of pending tasks to running tasks on Yarn.                |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNAppRunning                           | Integer         | Number of running tasks on Yarn.                                                                             |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNContainerAllocated                   | Integer         | Number of containers allocated to Yarn.                                                                      |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNContainerPending                     | Integer         | Number of pending containers on Yarn.                                                                        |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNContainerPendingRatio                | Ratio           | Ratio of pending containers on Yarn, that is, the ratio of pending containers to running containers on Yarn. |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNCPUAllocated                         | Integer         | Number of virtual CPUs (vCPUs) allocated to Yarn                                                             |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNCPUAvailable                         | Integer         | Number of available vCPUs on Yarn.                                                                           |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNCPUAvailablePercentage               | Percentage      | Percentage of available vCPUs on Yarn, that is, the proportion of available vCPUs to total vCPUs.            |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100                                                                                        |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNCPUPending                           | Integer         | Number of pending vCPUs on Yarn.                                                                             |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNMemoryAllocated                      | Integer         | Memory allocated to Yarn. The unit is MB.                                                                    |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNMemoryAvailable                      | Integer         | Available memory on Yarn. The unit is MB.                                                                    |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNMemoryAvailablePercentage            | Percentage      | Percentage of available memory on Yarn, that is, the proportion of available memory to total memory on Yarn. |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100                                                                                        |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNMemoryPending                        | Integer         | Pending memory on Yarn.                                                                                      |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646                                                                                 |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+

.. note::

   When the value type is percentage or ratio in :ref:`Table 14 <mrs_02_0028__t27de3279a99a48968dacb015c498d9cb>`, the valid value can be accurate to percentile. The percentage metric value is a decimal value with a percent sign (%) removed. For example, 16.80 represents 16.80%.

.. _mrs_02_0028__table1258382865010:

.. table:: **Table 15** **bootstrap_scripts** parameter description

   +------------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter              | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
   +========================+=================+=================+==========================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
   | name                   | Yes             | String          | Name of a bootstrap action script. It must be unique in a cluster.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | The value can contain only digits, letters, spaces, hyphens (-), and underscores (_) and cannot start with a space.                                                                                                                                                                                                                                                                                                                                                                                                      |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | The value can contain 1 to 64 characters.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
   +------------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | uri                    | Yes             | String          | Path of a bootstrap action script. Set this parameter to an OBS bucket path or a local VM path.                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | -  OBS bucket path: Enter a script path manually. For example, enter the path of the public sample script provided by MRS. Example: **s3a://bootstrap/presto/presto-install.sh**. If **dualroles** is installed, the parameter of the **presto-install.sh** script is **dualroles**. If **worker** is installed, the parameter of the **presto-install.sh** script is **worker**. Based on the Presto usage habit, you are advised to install **dualroles** on the active Master nodes and **worker** on the Core nodes. |
   |                        |                 |                 | -  Local VM path: Enter a script path. The script path must start with a slash (/) and end with **.sh**.                                                                                                                                                                                                                                                                                                                                                                                                                 |
   +------------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | parameters             | No              | String          | Bootstrap action script parameters.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
   +------------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | nodes                  | Yes             | Array String    | Type of a node where the bootstrap action script is executed. The value can be **Master**, **Core**, or **Task**.                                                                                                                                                                                                                                                                                                                                                                                                        |
   +------------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | active_master          | No              | Boolean         | Whether the bootstrap action script runs only on active Master nodes.                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | The default value is **false**, indicating that the bootstrap action script can run on all Master nodes.                                                                                                                                                                                                                                                                                                                                                                                                                 |
   +------------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | before_component_start | No              | Boolean         | Time when the bootstrap action script is executed. Currently, the following two options are available: **Before component start** and **After component start**                                                                                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | The default value is **false**, indicating that the bootstrap action script is executed after the component is started.                                                                                                                                                                                                                                                                                                                                                                                                  |
   +------------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | fail_action            | Yes             | String          | Whether to continue executing subsequent scripts and creating a cluster after the bootstrap action script fails to be executed.                                                                                                                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | -  **continue**: Continue to execute subsequent scripts.                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
   |                        |                 |                 | -  **errorout**: Stop the action.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | The default value is **errorout**, indicating that the action is stopped.                                                                                                                                                                                                                                                                                                                                                                                                                                                |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 |    You are advised to set this parameter to **continue** in the commissioning phase so that the cluster can continue to be installed and started no matter whether the bootstrap action is successful.                                                                                                                                                                                                                                                                                                                   |
   +------------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response
--------

.. table:: **Table 16** Response parameter description

   +-----------------------+-----------------------+---------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                               |
   +=======================+=======================+===========================================================================+
   | cluster_id            | String                | Cluster ID, which is returned by the system after the cluster is created. |
   +-----------------------+-----------------------+---------------------------------------------------------------------------+
   | result                | Bool                  | Operation result.                                                         |
   |                       |                       |                                                                           |
   |                       |                       | -  **true**: The operation is successful.                                 |
   |                       |                       | -  **false**: The operation failed.                                       |
   +-----------------------+-----------------------+---------------------------------------------------------------------------+
   | msg                   | String                | System message, which can be empty.                                       |
   +-----------------------+-----------------------+---------------------------------------------------------------------------+

Example
-------

-  Example request

   -  Creating a cluster with **Cluster HA** enabled (using the **node_groups** parameter group)

      .. code-block::

         {
             "billing_type": 12,
             "data_center": "eu-de",
             "available_zone_id": "bf84aba586ce4e948da0b97d9a7d62fb",
             "cluster_name": "mrs_HEbK",
             "cluster_version": "MRS 3.X.X",
             "safe_mode": 0,
             "cluster_type": 0,
         "component_list": [
                 {
                     "component_name": "Hadoop"
                 },
                 {
                     "component_name": "Spark"
                 },
                 {
                     "component_name": "HBase"
                 },
                 {
                     "component_name": "Hive"
                 },
                 {
                     "component_name": "Presto"
                 },
                 {
                     "component_name": "Tez"
                 },
                 {
                      "component_name": "Hue"
                 },
                 {
                     "component_name": "Loader"
                 },
                 {
                     "component_name": "Flink"
                  }
         ],
             "vpc": "vpc-4b1c",
             "vpc_id": "4a365717-67be-4f33-80c5-98e98a813af8",
             "subnet_id": "67984709-e15e-4e86-9886-d76712d4e00a",
             "subnet_name": "subnet-4b44",
             "security_groups_id": "4820eace-66ad-4f2c-8d46-cf340e3029dd",
             "tags": [{
                 "key": "key1",
                 "value": "value1"
             }, {
                 "key": "key2",
                 "value": "value2"
             }],
             "node_groups": [{
                     "group_name": "master_node_default_group",
                     "node_num": 2,
                     "node_size": "c6.4.xlarge.4linux.mrs",
                     "root_volume_size": 480,
                     "root_volume_type": "SATA",
                     "data_volume_type": "SATA",
                     "data_volume_count": 1,
                     "data_volume_size": 600
                 }, {
                     "group_name": "core_node_analysis_group",
                     "node_num": 3,
                     "node_size": "c6.4.xlarge.4linux.mrs",
                     "root_volume_size": 480,
                     "root_volume_type": "SATA",
                     "data_volume_type": "SATA",
                     "data_volume_count": 1,
                     "data_volume_size": 600
                 }, {
                     "group_name": "task_node_analysis_group",
                     "node_num": 2,
                     "node_size": "c6.4.xlarge.4linux.mrs",
                     "root_volume_size": 480,
                     "root_volume_type": "SATA",
                     "data_volume_type": "SATA",
                     "data_volume_count": 0,
                     "data_volume_size": 600,
                     "auto_scaling_policy": {
                         "auto_scaling_enable": true,
                         "min_capacity": 1,
                         "max_capacity": "3",
                         "resources_plans": [{
                             "period_type": "daily",
                             "start_time": "9:50",
                             "end_time": "10:20",
                             "min_capacity": 2,
                             "max_capacity": 3
                         }, {
                             "period_type ": "daily",
                             "start_time ": "10:20",
                             "end_time ": "12:30",
                             "min_capacity ": 0,
                             "max_capacity ": 2
                         }],
                         "exec_scripts": [{
                             "name": "before_scale_out",
                             "uri": "s3a://XXX/zeppelin_install.sh ",
                             "parameters": "${mrs_scale_node_num} ${mrs_scale_type} xxx",
                             "nodes": ["master", "core", "task"],
                             "active_master": "true",
                             "action_stage": "before_scale_out",
                             "fail_sction": "continue"
                         }, {
                             "name": "after_scale_out",
                             "uri": "s3a://XXX/storm_rebalance.sh",
                             "parameters": "${mrs_scale_node_hostnames} ${mrs_scale_node_ips}",
                             "nodes": ["master", "core", "task"],
                             "active_master": "true",
                             "action_stage": "after_scale_out",
                             "fail_action": "continue"
                         }],
                         "rules": [{
                             "name": "default-expand-1",
                             "adjustment_type": "scale_out",
                             "cool_down_minutes": 5,
                             "scaling_adjustment": 1,
                             "trigger": {
                                 "metric_name": "YARNMemoryAvailablePercentage",
                                 "metric_value": "25",
                                 "comparison_operator": "LT",
                                 "evaluation_periods": 10
                             }
                         }, {
                             "name": "default-shrink-1",
                             "adjustment_type": "scale_in",
                             "cool_down_minutes": 5,
                             "scaling_adjustment": 1,
                             "trigger": {
                                 "metric_name": "YARNMemoryAvailablePercentage",
                                 "metric_value": "70",
                                 "comparison_operator": "GT",
                                 "evaluation_periods": 10
                             }
                         }]
                     }
                 }
             ],
             "login_mode": 1,
             "cluster_master_secret": "",
             "cluster_admin_secret": "",
             "log_collection": 1,
             "add_jobs": [{
                 "job_type": 1,
                 "job_name": "tenji111",
                 "jar_path": "s3a://bigdata/program/hadoop-mapreduce-examples-2.7.2.jar",
                 "arguments": "wordcount",
                 "input": "s3a://bigdata/input/wd_1k/",
                 "output": "s3a://bigdata/ouput/",
                 "job_log": "s3a://bigdata/log/",
                 "shutdown_cluster": true,
                 "file_action": "",
                 "submit_job_once_cluster_run": true,
                 "hql": "",
                 "hive_script_path": ""
             }],
             "bootstrap_scripts": [{
                 "name": "Modify os config",
                 "uri": "s3a://XXX/modify_os_config.sh",
                 "parameters": "param1 param2",
                 "nodes": ["master", "core", "task"],
                 "active_master": "false",
                 "before_component_start": "true",
                 "fail_action": "continue"
             }, {
                 "name": "Install zepplin",
                 "uri": "s3a://XXX/zeppelin_install.sh",
                 "parameters": "",
                 "nodes": ["master"],
                 "active_master": "true",
                 "before_component_start": "false",
                 "fail_action": "continue"
             }]
         }

   -  Creating a cluster with **Cluster HA** enabled (without using the **node_groups** parameter group)

      .. code-block::

         {
             "billing_type": 12,
             "data_center": "eu-de",
             "master_node_num": 2,
             "master_node_size": "s1.8xlarge.linux.mrs",
             "core_node_num": 3,
             "core_node_size": "c6.4xlarge.4linux.mrs",
             "available_zone_id": "bf84aba586ce4e948da0b97d9a7d62fb",
             "cluster_name": "newcluster",
             "vpc": "vpc1",
             "vpc_id": "5b7db34d-3534-4a6e-ac94-023cd36aaf74",
             "subnet_id": "815bece0-fd22-4b65-8a6e-15788c99ee43",
             "subnet_name": "subnet",
             "security_groups_id": "",
             "tags": [
                {
                   "key": "key1",
                   "value": "value1"
                },
                {
                   "key": "key2",
                   "value": "value2"
                }
             ],
             "cluster_version": "MRS 3.X.X",
             "cluster_type": 0,
             "master_data_volume_type": "SATA",
             "master_data_volume_size": 100,
             "master_data_volume_count": 1,
             "core_data_volume_type": "SATA",
             "core_data_volume_size": 100,
             "core_data_volume_count": 2,
             "login_mode": 1,
             "node_public_cert_name": "SSHkey-bba1",
             "safe_mode": 0,
             "cluster_admin_secret":"******",
             "log_collection": 1,
             "task_node_groups": [
                {

                  "node_num": 2,
                  "node_size": "c6.4.xlarge.4linux.mrs",
                  "data_volume_type": "SATA",
                  "data_volume_count": 1,
                  "data_volume_size": 600,
                  "auto_scaling_policy":
                   {
                      "auto_scaling_enable": true,
                      "min_capacity": "1",
                      "max_capacity": "3",
                      "resources_plans": [{
                        "period_type": "daily",
                        "start_time": "9:50",
                        "end_time": "10:20",
                        "min_capacity": "2",
                        "max_capacity": "3"
                      },{
                        "period_type": "daily",
                        "start_time": "10:20",
                        "end_time": "12:30",
                        "min_capacity": "0",
                        "max_capacity": "2"
                      }],
                      "exec_scripts": [{
                        "name": "before_scale_out",
                        "uri": "s3a://XXX/zeppelin_install.sh",
                        "parameters": "",
                        "nodes": [
                          "master",
                          "core",
                          "task"
                        ],
                        "active_master": "true",
                        "action_stage": "before_scale_out",
                        "fail_action": "continue"
                      },{
                        "name": "after_scale_out",
                        "uri": "s3a://XXX/storm_rebalance.sh",
                        "parameters": "",
                        "nodes": [
                          "master",
                          "core",
                          "task"
                        ],
                        "active_master": "true",
                        "action_stage": "after_scale_out",
                        "fail_action": "continue"
                      }],
                      "rules": [
                       {
                        "name": "default-expand-1",
                        "adjustment_type": "scale_out",
                        "cool_down_minutes": 5,
                        "scaling_adjustment": 1,
                        "trigger": {
                          "metric_name": "YARNMemoryAvailablePercentage",
                          "metric_value": "25",
                          "comparison_operator": "LT",
                          "evaluation_periods": 10
                         }
                        },
                      {
                        "name": "default-shrink-1",
                        "adjustment_type": "scale_in",
                        "cool_down_minutes": 5,
                        "scaling_adjustment": 1,
                        "trigger": {
                          "metric_name": "YARNMemoryAvailablePercentage",
                          "metric_value": "70",
                          "comparison_operator": "GT",
                          "evaluation_periods": 10
                        }
                      }
                    ]
                  }
                }
              ],
             "component_list": [
                {
                     "component_name": "Hadoop"
                 },
                 {
                     "component_name": "Spark"
                 },
                 {
                     "component_name": "HBase"
                 },
                 {
                     "component_name": "Hive"
                 },
                 {
                     "component_name": "Presto"
                 },
                 {
                     "component_name": "Tez"
                 },
                 {
                      "component_name": "Hue"
                 },
                 {
                     "component_name": "Loader"
                 },
                 {
                     "component_name": "Flink"
                  }
             ],
             "add_jobs": [
                 {
                     "job_type": 1,
                     "job_name": "tenji111",
                     "jar_path": "s3a://bigdata/program/hadoop-mapreduce-examples-XXX.jar",
                     "arguments": "wordcount",
                     "input": "s3a://bigdata/input/wd_1k/",
                     "output": "s3a://bigdata/ouput/",
                     "job_log": "s3a://bigdata/log/",
                     "shutdown_cluster": false,
                     "file_action": "",
                     "submit_job_once_cluster_run": true,
                     "hql": "",
                     "hive_script_path": ""
                 }
             ],
         "bootstrap_scripts": [
                  {
                      "name":"Modify os config",
                      "uri":"s3a://XXX/modify_os_config.sh",
                      "parameters":"param1 param2",
                      "nodes":[
                          "master",
                          "core",
                          "task"
                      ],
                      "active_master":"false",
                      "before_component_start":"true",
                      "fail_action":"continue"
                  },
                  {
                      "name":"Install zepplin",
                      "uri":"s3a://XXX/zeppelin_install.sh",
                      "parameters":"",
                      "nodes":[
                          "master"
                      ],
                      "active_master":"true",
                      "before_component_start":"false",
                      "fail_action":"continue"
                  }
              ]
         }

   -  Disabling the **Cluster HA** function and creating a cluster with the minimum specifications (using the **node_groups** parameter group)

      .. code-block::

         {
             "billing_type": 12,
             "data_center": "eu-de",
             "available_zone_id": "bf84aba586ce4e948da0b97d9a7d62fb",
             "cluster_name": "mrs_HEbK",
             "cluster_version": "MRS 3.X.X",
             "safe_mode": 0,
             "cluster_type": 0,
         "component_list": [
                 {
                     "component_name": "Hadoop"
                 },
                 {
                     "component_name": "Spark"
                 },
                 {
                     "component_name": "HBase"
                 },
                 {
                     "component_name": "Hive"
                 },
                 {
                     "component_name": "Presto"
                 },
                 {
                     "component_name": "Tez"
                 },
                 {
                      "component_name": "Hue"
                 },
                 {
                     "component_name": "Loader"
                 },
                 {
                     "component_name": "Flink"
                  }
         ],
             "vpc": "vpc-4b1c",
             "vpc_id": "4a365717-67be-4f33-80c5-98e98a813af8",
             "subnet_id": "67984709-e15e-4e86-9886-d76712d4e00a",
             "subnet_name": "subnet-4b44",
             "security_groups_id": "4820eace-66ad-4f2c-8d46-cf340e3029dd",
             "tags": [{
                 "key": "key1",
                 "value": "value1"
             }, {
                 "key": "key2",
                 "value": "value2"
             }],
             "node_groups": [{
                     "group_name": "master_node_default_group",
                     "node_num": 1,
                     "node_size": "c6.4.xlarge.4linux.mrs",
                     "root_volume_size": 480,
                     "root_volume_type": "SATA",
                     "data_volume_type": "SATA",
                     "data_volume_count": 1,
                     "data_volume_size": 600
                 }, {
                     "group_name": "core_node_analysis_group",
                     "node_num": 1,
                     "node_size": "c6.4.xlarge.4linux.mrs",
                     "root_volume_size": 480,
                     "root_volume_type": "SATA",
                     "data_volume_type": "SATA",
                     "data_volume_count": 1,
                     "data_volume_size": 600
                 }
             ],
             "login_mode": 1,
             "cluster_master_secret": "",
             "cluster_admin_secret": "",
             "log_collection": 1,
             "add_jobs": [{
                 "job_type": 1,
                 "job_name": "tenji111",
                 "jar_path": "s3a://bigdata/program/hadoop-mapreduce-examples-2.7.2.jar",
                 "arguments": "wordcount",
                 "input": "s3a://bigdata/input/wd_1k/",
                 "output": "s3a://bigdata/ouput/",
                 "job_log": "s3a://bigdata/log/",
                 "shutdown_cluster": true,
                 "file_action": "",
                 "submit_job_once_cluster_run": true,
                 "hql": "",
                 "hive_script_path": ""
             }],
             "bootstrap_scripts": [{
                 "name": "Modify os config",
                 "uri": "s3a://XXX/modify_os_config.sh",
                 "parameters": "param1 param2",
                 "nodes": ["master", "core", "task"],
                 "active_master": "false",
                 "before_component_start": "true",
                 "fail_action": "continue"
             }, {
                 "name": "Install zepplin",
                 "uri": "s3a://XXX/zeppelin_install.sh",
                 "parameters": "",
                 "nodes": ["master"],
                 "active_master": "true",
                 "before_component_start": "false",
                 "fail_action": "continue"
             }]
         }

   -  Disabling the **Cluster HA** function and creating a cluster with the minimum specifications (without using the **node_groups** parameter group)

      .. code-block::

         {
             "billing_type": 12,
             "data_center": "eu-de",
             "master_node_num": 1
             "master_node_size": "s1.8xlarge.linux.mrs",
             "core_node_num": 1,
             "core_node_size": "c6.4xlarge.4linux.mrs",
             "available_zone_id": "bf84aba586ce4e948da0b97d9a7d62fb",
             "cluster_name": "newcluster",
             "vpc": "vpc1",
             "vpc_id": "5b7db34d-3534-4a6e-ac94-023cd36aaf74",
             "subnet_id": "815bece0-fd22-4b65-8a6e-15788c99ee43",
             "subnet_name": "subnet",
             "security_groups_id": "",
             "tags": [
                {
                   "key": "key1",
                   "value":"value1"
                },
                {
                   "key": "key2",
                   "value": "value2"
                }
             ],
             "cluster_version": "MRS 3.X.X",
             "cluster_type": 0,
             "master_data_volume_type": "SATA",
             "master_data_volume_size": 100,
             "master_data_volume_count": 1,
             "core_data_volume_type": "SATA",
             "core_data_volume_size": 100,
             "core_data_volume_count": 1,
             "login_mode": 1,
             "node_public_cert_name": "SSHkey-bba1",
             "safe_mode": 0,
             "cluster_admin_secret":"******",
             "log_collection": 1,
             "component_list": [
                 {
                    "component_name": "Hadoop"
                  },
                 {
                    "component_name": "Spark"
                  },
                 {
                    "component_name": "HBase"
                  },
                 {
                     "component_name": "Hive"
                  },
                 {
                      "component_name": "Presto"
                   },
                 {
                     "component_name": "Tez"
                 },
                 {
                     "component_name": "Hue"
                 },
                 {
                     "component_name": "Loader"
                 },
                 {
                     "component_name": "Flink"
                 }
                               ],
             "add_jobs": [
                 {
                     "job_type": 1,
                     "job_name": "tenji111",
                     "jar_path": "s3a://bigdata/program/hadoop-mapreduce-examples-XXX.jar",
                     "arguments": "wordcount",
                     "input": "s3a://bigdata/input/wd_1k/",
                     "output": "s3a://bigdata/ouput/",
                     "job_log": "s3a://bigdata/log/",
                     "shutdown_cluster": false,
                     "file_action": "",
                     "submit_job_once_cluster_run": true,
                     "hql": "",
                     "hive_script_path": ""
                 }
             ],
         "bootstrap_scripts": [
                  {
                      "name":"Install zepplin",
                      "uri":"s3a://XXX/zeppelin_install.sh",
                      "parameters":"",
                      "nodes":[
                      "master"
                      ],
                      "active_master":"false",
                      "before_component_start":"false",
                      "fail_action":"continue"
                  }
             ]
         }

-  Example response

   .. code-block::

      {
          "cluster_id": "da1592c2-bb7e-468d-9ac9-83246e95447a",
          "result": true,
          "msg": ""
      }

Status Code
-----------

:ref:`Table 17 <mrs_02_0028__t9da59f1e3aaa4a09903f34b2fc2401e4>` describes the status code of this API.

.. _mrs_02_0028__t9da59f1e3aaa4a09903f34b2fc2401e4:

.. table:: **Table 17** Status code

   =========== ==========================================
   Status Code Description
   =========== ==========================================
   200         The cluster has been successfully created.
   =========== ==========================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
