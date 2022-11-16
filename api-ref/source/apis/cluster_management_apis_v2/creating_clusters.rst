:original_name: mrs_02_0101.html

.. _mrs_02_0101:

Creating Clusters
=================

Function
--------

This API is used to create an MRS cluster.

Before using the API, you need to obtain the resources listed in :ref:`Table 1 <mrs_02_0101__tbbd2986d18874f82a8ab886ac25a57f8>`.

.. _mrs_02_0101__tbbd2986d18874f82a8ab886ac25a57f8:

.. table:: **Table 1** Obtaining resources

   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Resource                          | How to Obtain                                                                                                                                                                         |
   +===================================+=======================================================================================================================================================================================+
   | VPC                               | See operation instructions in **VPC > Querying VPCs** and **VPC > Creating a VPC** in the *VPC API Reference*.                                                                        |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Subnet                            | See operation instructions in **Subnet > Querying Subnets** and **Subnet > Creating a Subnet** in the *VPC API Reference*.                                                            |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Key Pair                          | See operation instructions in **ECS SSH Key Management > Querying SSH Key Pairs** and **ECS SSH Key Management > Creating and Importing an SSH Key Pair** in the *ECS API Reference*. |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Zone                              | Obtain the region and AZ information. For more information about regions and AZs, see `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__.           |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Version                           | Currently, MRS 1.6.3, MRS 1.7.2, MRS 1.9.2 MRS 2.1.0, MRS 3.1.0-LTS.1 and MRS 3.1.2-LTS.3 are supported.                                                                              |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Component                         | -  MRS 3.1.2-LTS.3 supports the following components:                                                                                                                                 |
   |                                   |                                                                                                                                                                                       |
   |                                   |    -  The analysis cluster contains the following components: Hadoop, Spark2x, HBase, Hive, Hue, HetuEngine, Loader, Flink, Oozie, ZooKeeper, Ranger, and Tez.                        |
   |                                   |    -  The streaming cluster contains the following components: Kafka, Flume, ZooKeeper, and Ranger.                                                                                   |
   |                                   |    -  The hybrid cluster contains the following components: Hadoop, Spark2x, HBase, Hive, Hue, HetuEngine, Loader, Flink, Oozie, ZooKeeper, Ranger, Tez, Kafka, and Flume.            |
   |                                   |    -  A custom cluster contains the following components: Hadoop, Spark2x, HBase, Hive, Hue, HetuEngine, Loader, Kafka, Flume, Flink, Oozie, ZooKeeper, Ranger, Tez, and ClickHouse.  |
   |                                   |                                                                                                                                                                                       |
   |                                   | -  MRS 3.1.0-LTS.1 supports the following components:                                                                                                                                 |
   |                                   |                                                                                                                                                                                       |
   |                                   |    -  The analysis cluster contains the following components: Hadoop, Spark2x, HBase, Hive, Hue, HetuEngine, Loader, Flink, Oozie, ZooKeeper, Ranger, and Tez.                        |
   |                                   |    -  The streaming cluster contains the following components: Kafka, Flume, ZooKeeper, and Ranger.                                                                                   |
   |                                   |    -  The hybrid cluster contains the following components: Hadoop, Spark2x, HBase, Hive, Hue, HetuEngine, Loader, Flink, Oozie, ZooKeeper, Ranger, Tez, Kafka, and Flume.            |
   |                                   |    -  A custom cluster contains the following components: Hadoop, Spark2x, HBase, Hive, Hue, HetuEngine, Loader, Kafka, Flume, Flink, Oozie, ZooKeeper, Ranger, and Tez.              |
   |                                   |                                                                                                                                                                                       |
   |                                   | -  MRS 2.1.0 supports the following components:                                                                                                                                       |
   |                                   |                                                                                                                                                                                       |
   |                                   |    -  The analysis cluster contains the following components: Presto, Hadoop, Spark, HBase, Hive, Hue, Loader, Tez, Flink.                                                            |
   |                                   |    -  The streaming cluster contains the following components: Kafka, Storm, and Flume.                                                                                               |
   |                                   |    -  The hybrid cluster contains the following components: Hadoop, Hive, Presto, Spark, Tez, and Flink.                                                                              |
   |                                   |                                                                                                                                                                                       |
   |                                   | -  MRS 1.9.2 supports the following components:                                                                                                                                       |
   |                                   |                                                                                                                                                                                       |
   |                                   |    -  The analysis cluster contains the following components: Presto, Hadoop, Spark, HBase, Opentsdb, Hive, Hue, Loader, Tez, Flink, Alluxio and Ranger                               |
   |                                   |    -  The streaming cluster contains the following components: Kafka, KafkaManager, Storm, and Flume.                                                                                 |
   |                                   |    -  The hybrid cluster contains the following components: Hadoop, Hive, Presto, Spark, Tez, Kafka, Flink, and Ranger.                                                               |
   |                                   |                                                                                                                                                                                       |
   |                                   | -  MRS 1.7.2 and MRS 1.6.3 support the following components:                                                                                                                          |
   |                                   |                                                                                                                                                                                       |
   |                                   |    -  The analysis cluster contains the following components: Hadoop, Spark, HBase, Hive, Hue, and Loader                                                                             |
   |                                   |    -  The streaming cluster contains the following components: Kafka, Storm, and Flume.                                                                                               |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

URI
---

-  URI format

   POST /v2/{project_id}/clusters

-  Parameters

   .. table:: **Table 2** URI parameter

      +------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | Name       | Mandatory | Description                                                                                               |
      +============+===========+===========================================================================================================+
      | project_id | Yes       | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
      +------------+-----------+-----------------------------------------------------------------------------------------------------------+

Request
-------

.. table:: **Table 3** Parameter description

   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter              | Mandatory       | Type                     | Description                                                                                                                                                                                                                                                                                                                                                                                 |
   +========================+=================+==========================+=============================================================================================================================================================================================================================================================================================================================================================================================+
   | cluster_version        | Yes             | String                   | Cluster version.                                                                                                                                                                                                                                                                                                                                                                            |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | Possible values are as follows:                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | -  MRS 1.6.3                                                                                                                                                                                                                                                                                                                                                                                |
   |                        |                 |                          | -  MRS 1.7.2                                                                                                                                                                                                                                                                                                                                                                                |
   |                        |                 |                          | -  MRS 1.9.2                                                                                                                                                                                                                                                                                                                                                                                |
   |                        |                 |                          | -  MRS 2.1.0                                                                                                                                                                                                                                                                                                                                                                                |
   |                        |                 |                          | -  MRS 3.1.0-LTS.1                                                                                                                                                                                                                                                                                                                                                                          |
   |                        |                 |                          | -  MRS 3.1.2-LTS.3                                                                                                                                                                                                                                                                                                                                                                          |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | cluster_name           | Yes             | String                   | Cluster name. It must be unique.                                                                                                                                                                                                                                                                                                                                                            |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | A cluster name can contain only 2 to 64 characters. Only letters, digits, hyphens (-), and underscores (_) are allowed.                                                                                                                                                                                                                                                                     |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | cluster_type           | Yes             | String                   | Cluster type. The options are as follows:                                                                                                                                                                                                                                                                                                                                                   |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | -  **ANALYSIS**: analysis cluster                                                                                                                                                                                                                                                                                                                                                           |
   |                        |                 |                          | -  **STREAMING**: streaming cluster                                                                                                                                                                                                                                                                                                                                                         |
   |                        |                 |                          | -  **MIXED**: hybrid cluster                                                                                                                                                                                                                                                                                                                                                                |
   |                        |                 |                          | -  **CUSTOM**: customized cluster, which is supported only by MRS 3.x.x.                                                                                                                                                                                                                                                                                                                    |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | charge_info            | No              | ChargeInfo               | Charging type information. For details, see :ref:`Table 6 <mrs_02_0101__table1164193817438>`.                                                                                                                                                                                                                                                                                               |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | region                 | Yes             | String                   | Region of the cluster. For details, see `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__.                                                                                                                                                                                                                                                               |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | vpc_name               | Yes             | String                   | Name of the VPC where the subnet locates                                                                                                                                                                                                                                                                                                                                                    |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | Perform the following operations to obtain the VPC name from the VPC management console:                                                                                                                                                                                                                                                                                                    |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | #. Log in to the management console.                                                                                                                                                                                                                                                                                                                                                        |
   |                        |                 |                          | #. Click **Virtual Private Cloud** and select **Virtual Private Cloud** from the left list.                                                                                                                                                                                                                                                                                                 |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | On the **Virtual Private Cloud** page, obtain the VPC name from the list.                                                                                                                                                                                                                                                                                                                   |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | subnet_name            | Yes             | String                   | Subnet name.                                                                                                                                                                                                                                                                                                                                                                                |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | Perform the following operations to obtain the subnet name from the VPC management console:                                                                                                                                                                                                                                                                                                 |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | #. Log in to the management console.                                                                                                                                                                                                                                                                                                                                                        |
   |                        |                 |                          | #. Click **Virtual Private Cloud** and select **Virtual Private Cloud** from the left list.                                                                                                                                                                                                                                                                                                 |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | On the **Virtual Private Cloud** page, obtain the subnet name of the VPC from the list.                                                                                                                                                                                                                                                                                                     |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | components             | Yes             | String                   | List of component names, which are separated by commas (,). For details about the component names, see the component list of each version in Table 4-1.                                                                                                                                                                                                                                     |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | availability_zone      | Yes             | String                   | Name of an AZ.                                                                                                                                                                                                                                                                                                                                                                              |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | AZ information. For details, see `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__.                                                                                                                                                                                                                                                                      |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | security_groups_id     | No              | String                   | Security group ID of the cluster                                                                                                                                                                                                                                                                                                                                                            |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | -  If this parameter is left blank, MRS automatically creates a security group, whose name starts with **mrs_{cluster_name}**.                                                                                                                                                                                                                                                              |
   |                        |                 |                          | -  If this parameter is not left blank, a fixed security group is used to create a cluster. The transferred ID must be the security group ID owned by the current tenant. The security group must include an inbound rule in which all protocols and all ports are allowed and the source is the IP address of the specified node on the management plane.                                  |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | safe_mode              | Yes             | String                   | Running mode of an MRS cluster                                                                                                                                                                                                                                                                                                                                                              |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | -  **SIMPLE**: normal cluster. In a normal cluster, Kerberos authentication is disabled, and users can use all functions provided by the cluster.                                                                                                                                                                                                                                           |
   |                        |                 |                          | -  **KERBEROS**: security cluster. In a security cluster, Kerberos authentication is enabled, and common users cannot use the file management and job management functions of an MRS cluster or view cluster resource usage and the job records of Hadoop and Spark. To use more cluster functions, the users must contact the Manager administrator to assign more permissions.            |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | manager_admin_password | Yes             | String                   | Password of the MRS Manager administrator.                                                                                                                                                                                                                                                                                                                                                  |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | -  Must be a string and 8 to 32 characters long.                                                                                                                                                                                                                                                                                                                                            |
   |                        |                 |                          | -  The password must contain at least three types of the following characters (if the value of cluster_version is FusionInsight 6.5.1, the password must contain at least four types of the following characters):                                                                                                                                                                          |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          |    -  Lowercase letters                                                                                                                                                                                                                                                                                                                                                                     |
   |                        |                 |                          |    -  Uppercase letters                                                                                                                                                                                                                                                                                                                                                                     |
   |                        |                 |                          |    -  Digits                                                                                                                                                                                                                                                                                                                                                                                |
   |                        |                 |                          |    -  Special characters: :literal:`\`~!@#$%^&*()-_=+\\|[{}];:'",<.>/?`                                                                                                                                                                                                                                                                                                                     |
   |                        |                 |                          |    -  Spaces                                                                                                                                                                                                                                                                                                                                                                                |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | -  Cannot be the username or the username spelled backwards.                                                                                                                                                                                                                                                                                                                                |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          |    .. note::                                                                                                                                                                                                                                                                                                                                                                                |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          |       For MRS 1.7.2 or earlier, this parameter is mandatory only when **safe_mode** is set to **KERBEROS**.                                                                                                                                                                                                                                                                                 |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | login_mode             | Yes             | String                   | Node login mode.                                                                                                                                                                                                                                                                                                                                                                            |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | -  **PASSWORD**: password-based login. If this value is selected, **node_root_password** cannot be left blank.                                                                                                                                                                                                                                                                              |
   |                        |                 |                          | -  **KEYPAIR**: specifies the key pair used for login. If this value is selected, **node_keypair_name** cannot be left blank.                                                                                                                                                                                                                                                               |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | node_root_password     | No              | String                   | Password of user **root** for logging in to a cluster node                                                                                                                                                                                                                                                                                                                                  |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | A password must meet the following requirements:                                                                                                                                                                                                                                                                                                                                            |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | -  Must be a string and 8 to 26 characters long.                                                                                                                                                                                                                                                                                                                                            |
   |                        |                 |                          | -  Must contain at least three of the following: uppercase letters, lowercase letters, digits, and special characters (``!@$%^-_=+[{}]:,./?``), but must not contain spaces.                                                                                                                                                                                                                |
   |                        |                 |                          | -  Cannot be the username or the username spelled backwards.                                                                                                                                                                                                                                                                                                                                |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | node_keypair_name      | No              | String                   | Name of a key pair You can use a key pair to log in to the Master node in the cluster.                                                                                                                                                                                                                                                                                                      |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | log_collection         | No              | Integer                  | Whether to collect logs when cluster creation fails                                                                                                                                                                                                                                                                                                                                         |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | -  **0**: Do not collect.                                                                                                                                                                                                                                                                                                                                                                   |
   |                        |                 |                          | -  **1**: Collect.                                                                                                                                                                                                                                                                                                                                                                          |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | The default value is **1**, indicating that OBS buckets will be created and only used to collect logs that record MRS cluster creation failures.                                                                                                                                                                                                                                            |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | eip_address            | No              | String                   | An EIP bound to an MRS cluster can be used to access MRS Manager. The EIP must have been created and must be in the same region as the cluster.                                                                                                                                                                                                                                             |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | mrs_ecs_default_agency | No              | String                   | Name of the agency bound to a cluster node by default. The value is fixed to **MRS_ECS_DEFAULT_AGENCY**.                                                                                                                                                                                                                                                                                    |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | An agency allows ECS or BMS to manage MRS resources. You can configure an agency of the ECS type to automatically obtain the AK/SK to access OBS.                                                                                                                                                                                                                                           |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | The **MRS_ECS_DEFAULT_AGENCY** agency has the OBS OperateAccess permission of OBS and the CES FullAccess (for users who have enabled fine-grained policies), CES Administrator, and KMS Administrator permissions in the region where the cluster is located.                                                                                                                               |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | template_id            | No              | String                   | For **Custom** cluster type, it is used to specify the common node configurations used for deployment.                                                                                                                                                                                                                                                                                      |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | -  mgmt_control_combined_v2: indicates the **Compact** configuration. The management node and control node are deployed on the Master node, and data instances are deployed in the same node group. This deployment mode applies to scenarios where the number of control nodes is less than 100, reducing costs.                                                                           |
   |                        |                 |                          | -  mgmt_control_separated_v2: indicates the **OMS-separate** configuration. The management node and control node are deployed on different Master nodes, and data instances are deployed in the same node group. This deployment mode is applicable to a cluster with 100 to 500 control nodes and delivers better performance in high-concurrency load scenarios.                          |
   |                        |                 |                          | -  mgmt_control_data_separated_v2: indicates the **Full-size** configuration. The management node and control node are deployed on different Master nodes, and data instances are deployed in different node groups. This deployment mode is applicable to a cluster with more than 500 control nodes. Components can be deployed separately, which can be used for a larger cluster scale. |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | tags                   | No              | Array of Tag             | Cluster tag For more parameter description, see :ref:`Table 4 <mrs_02_0101__table16429741613>`.                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | A maximum of 10 tags can be added to a cluster.                                                                                                                                                                                                                                                                                                                                             |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | node_groups            | Yes             | Array of NodeGroup       | Information about the node groups in the cluster. For details about the parameters, see :ref:`Table 5 <mrs_02_0101__table3419221413>`.                                                                                                                                                                                                                                                      |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | bootstrap_scripts      | No              | Array of BootstrapScript | Bootstrap action script information. For more parameter description, see :ref:`Table 8 <mrs_02_0101__table1258382865010>`.                                                                                                                                                                                                                                                                  |
   |                        |                 |                          |                                                                                                                                                                                                                                                                                                                                                                                             |
   |                        |                 |                          | MRS 1.7.2 or later supports this parameter.                                                                                                                                                                                                                                                                                                                                                 |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | add_jobs               | No              | Array of AddJobReq       | Jobs can be submitted when a cluster is created. Currently, only one job can be created. For details about job parameters, see :ref:`Table 9 <mrs_02_0101__t8ded0b3ae11742cea98a467ce26fd093>`.                                                                                                                                                                                             |
   +------------------------+-----------------+--------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0101__table16429741613:

.. table:: **Table 4** Tag structure

   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                       |
   +=================+=================+=================+===================================================================================================================+
   | key             | Yes             | String          | Tag key.                                                                                                          |
   |                 |                 |                 |                                                                                                                   |
   |                 |                 |                 | -  It contains a maximum of 36 Unicode characters and cannot be an empty string.                                  |
   |                 |                 |                 | -  The tag key can contain only uppercase letters, lowercase letters, digits, hyphens (-), and underscores (_).   |
   |                 |                 |                 | -  The tag key of a resource must be unique.                                                                      |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------+
   | value           | Yes             | String          | Value.                                                                                                            |
   |                 |                 |                 |                                                                                                                   |
   |                 |                 |                 | -  The value can contain 0 to 43 unicode characters that can be blank.                                            |
   |                 |                 |                 | -  The tag value can contain only uppercase letters, lowercase letters, digits, hyphens (-), and underscores (_). |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0101__table3419221413:

.. table:: **Table 5** NodeGroup structure description

   +---------------------+-----------------+-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter           | Mandatory       | Type              | Description                                                                                                                                                                                                                                                              |
   +=====================+=================+===================+==========================================================================================================================================================================================================================================================================+
   | group_name          | Yes             | String            | Node group name. The value can contain a maximum of 64 characters, including uppercase and lowercase letters, arrays, hyphens (-), and underscores (_). The rules for configuring node groups are as follows:                                                            |
   |                     |                 |                   |                                                                                                                                                                                                                                                                          |
   |                     |                 |                   | -  **master_node_default_group**: Master node group, which must be included in all cluster types.                                                                                                                                                                        |
   |                     |                 |                   | -  **core_node_analysis_group**: analysis Core node group, which must be contained in the analysis cluster and hybrid cluster.                                                                                                                                           |
   |                     |                 |                   | -  **core_node_streaming_group**: indicates the streaming Core node group, which must be included in both streaming and hybrid clusters.                                                                                                                                 |
   |                     |                 |                   | -  **task_node_analysis_group**: Analysis Task node group. This node group can be selected for analysis clusters and hybrid clusters as required.                                                                                                                        |
   |                     |                 |                   | -  **task_node_streaming_group**: streaming Task node group. This node group can be selected for streaming clusters and hybrid clusters as required.                                                                                                                     |
   |                     |                 |                   | -  **node_group{x}**: node group of the customized cluster. You can add multiple node groups as required. A maximum of nine node groups can be added.                                                                                                                    |
   +---------------------+-----------------+-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | node_num            | Yes             | Integer           | Number of nodes. The value ranges from 0 to 500. The maximum number of Core and Task nodes is 500.                                                                                                                                                                       |
   +---------------------+-----------------+-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | node_size           | Yes             | String            | Instance specifications of a node. for example, **c6.4xlarge4.linux.mrs** MRS supports host specifications determined by CPU, memory, and disk space. For details about instance specifications, see :ref:`ECS Specifications Used by MRS <mrs_01_9005>`.                |
   +---------------------+-----------------+-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | root_volume         | No              | Volume            | Specifies the system disk information of the node. This parameter is optional for some VMs or the system disk of the BMS. This parameter is mandatory in other cases. For details about the parameter description, see :ref:`Table 7 <mrs_02_0101__table5775844185911>`. |
   +---------------------+-----------------+-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | data_volume         | No              | Volume            | Data disk information. This parameter is mandatory when **data_volume_count** is not 0. For details about this parameter, see Table 4-7.                                                                                                                                 |
   +---------------------+-----------------+-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | data_volume_count   | No              | Integer           | Number of data disks of a node.                                                                                                                                                                                                                                          |
   |                     |                 |                   |                                                                                                                                                                                                                                                                          |
   |                     |                 |                   | Value range: 0 to 10                                                                                                                                                                                                                                                     |
   +---------------------+-----------------+-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | charge_info         | No              | ChargeInfo        | Billing type of the node group. The billing types of Master and Core node groups are the same as those of the cluster. The billing type of the Task node group can be different from that of the cluster.                                                                |
   +---------------------+-----------------+-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | auto_scaling_policy | No              | AutoScalingPolicy | Autoscaling rule corresponding to the node group. For details about the parameters, see :ref:`Table 10 <mrs_02_0101__t6d6054a35d6342dc9dc5b3b8580fec7c>`.                                                                                                                |
   +---------------------+-----------------+-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | assigned_roles      | No              | Array of String   | When the cluster type is **CUSTOM**, this parameter is mandatory. You can specify the roles deployed in the node group. This parameter is a string array. Each string represents a role expression.                                                                      |
   |                     |                 |                   |                                                                                                                                                                                                                                                                          |
   |                     |                 |                   | Role expression definition:                                                                                                                                                                                                                                              |
   |                     |                 |                   |                                                                                                                                                                                                                                                                          |
   |                     |                 |                   | -  If the role is deployed on all nodes in the node group, set this parameter to *<role name>*, for example, **DataNode**.                                                                                                                                               |
   |                     |                 |                   | -  If the role is deployed on a specified subscript node in the node group: *<role name>:<index1>,<index2>..., <indexN>*, for example, **NameNode:1,2**. The subscript starts from 1.                                                                                    |
   |                     |                 |                   | -  Some roles support multi-instance deployment (that is, multiple instances of the same role are deployed on a node): *<role name>[<instance count>*], for example, **EsNode[9]**.                                                                                      |
   |                     |                 |                   |                                                                                                                                                                                                                                                                          |
   |                     |                 |                   | For details about available roles, see :ref:`Roles and components supported by MRS11 <mrs_02_0106>`.                                                                                                                                                                     |
   +---------------------+-----------------+-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0101__table1164193817438:

.. table:: **Table 6** ChargeInfo structure description

   +-----------------+-----------------+-----------------+-------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                         |
   +=================+=================+=================+=====================================+
   | charge_mode     | Yes             | String          | Billing mode                        |
   |                 |                 |                 |                                     |
   |                 |                 |                 | The value of this parameter can be: |
   |                 |                 |                 |                                     |
   |                 |                 |                 | -  **postPaid**                     |
   +-----------------+-----------------+-----------------+-------------------------------------+

.. _mrs_02_0101__table5775844185911:

.. table:: **Table 7** Volume field data structure description

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                  |
   +=================+=================+=================+==============================================================================+
   | type            | Yes             | String          | Disk Type                                                                    |
   |                 |                 |                 |                                                                              |
   |                 |                 |                 | The following disk types are supported:                                      |
   |                 |                 |                 |                                                                              |
   |                 |                 |                 | -  **SATA**: common I/O disk                                                 |
   |                 |                 |                 | -  **SAS**: high I/O disk                                                    |
   |                 |                 |                 | -  **SSD**: ultra-high I/O disk                                              |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+
   | size            | Yes             | Integer         | Specifies the data disk size, in GB. The value range is **10** to **32768**. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------+

.. _mrs_02_0101__table1258382865010:

.. table:: **Table 8** BootstrapScript structure description

   +------------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter              | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
   +========================+=================+=================+==========================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
   | name                   | Yes             | String          | Name of a bootstrap action script. It must be unique in a cluster.                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |                        |                 |                 | The value can contain only digits, letters, spaces, hyphens (-), and underscores (_) and must not start with a space.                                                                                                                                                                                                                                                                                                                                                                                                    |
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

.. _mrs_02_0101__t8ded0b3ae11742cea98a467ce26fd093:

.. table:: **Table 9** Parameters in AddJobReq

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
   | input                       | No              | String          | Address for inputting data                                                                                                                                |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | Files can be stored in HDFS or OBS. The path varies depending on the file system.                                                                         |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | -  OBS: The path must start with **s3a://**. Files or programs encrypted by KMS are not supported.                                                        |
   |                             |                 |                 | -  HDFS: The path starts with a slash (**/**).                                                                                                            |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | The parameter contains a maximum of 1,023 characters, excluding special characters such as ``;|&>'<$,`` and can be left blank.                            |
   +-----------------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | output                      | No              | String          | Address for outputting data                                                                                                                               |
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
   |                             |                 |                 | -  import                                                                                                                                                 |
   |                             |                 |                 | -  export                                                                                                                                                 |
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
   |                             |                 |                 | -  Contains a maximum of 1,023 characters, excluding special characters such as ``;|&><'$.`` The address cannot be empty or full of spaces.               |
   |                             |                 |                 | -  Files can be stored in HDFS or OBS. The path varies depending on the file system.                                                                      |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 |    -  OBS: The path must start with **s3a://**. Files or programs encrypted by KMS are not supported.                                                     |
   |                             |                 |                 |    -  HDFS: The path starts with a slash (**/**).                                                                                                         |
   |                             |                 |                 |                                                                                                                                                           |
   |                             |                 |                 | -  Ends with **.sql**. **sql** is case-insensitive.                                                                                                       |
   +-----------------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0101__t6d6054a35d6342dc9dc5b3b8580fec7c:

.. table:: **Table 10** AutoScalingPolicy structure

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
   | resources_plans     | No              | List            | Resource plan list. For details, see :ref:`Table 11 <mrs_02_0101__table10281451162111>`. If this parameter is left blank, the resource plan is disabled.                   |
   |                     |                 |                 |                                                                                                                                                                            |
   |                     |                 |                 | When auto scaling is enabled, either a resource plan or an auto scaling rule must be configured.                                                                           |
   |                     |                 |                 |                                                                                                                                                                            |
   |                     |                 |                 | MRS 1.6.3 or later supports this parameter.                                                                                                                                |
   +---------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | exec_scripts        | No              | List            | List of custom scaling automation scripts. For details, see :ref:`Table 12 <mrs_02_0101__table1921110172216>`. If this parameter is left blank, a hook script is disabled. |
   |                     |                 |                 |                                                                                                                                                                            |
   |                     |                 |                 | MRS 1.7.2 or later supports this parameter.                                                                                                                                |
   +---------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | rules               | No              | List            | List of auto scaling rules. For details, see :ref:`Table 13 <mrs_02_0101__t4c9e3e169631470d81d260543affb7e1>`.                                                             |
   |                     |                 |                 |                                                                                                                                                                            |
   |                     |                 |                 | When auto scaling is enabled, either a resource plan or an auto scaling rule must be configured.                                                                           |
   +---------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0101__table10281451162111:

.. table:: **Table 11** **resources_plan** parameter description

   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                               |
   +=================+=================+=================+===========================================================================================================================================================================================+
   | period_type     | Yes             | String          | Cycle type of a resource plan. Currently, only the following cycle type is supported:                                                                                                     |
   |                 |                 |                 |                                                                                                                                                                                           |
   |                 |                 |                 | -  daily                                                                                                                                                                                  |
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

.. _mrs_02_0101__table1921110172216:

.. table:: **Table 12** **exec_script** parameter description

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                                     |
   +=================+=================+=================+=================================================================================================================================================================================================================================+
   | name            | Yes             | String          | Name of a custom automation script. It must be unique in a same cluster.                                                                                                                                                        |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | The value can contain only digits, letters, spaces, hyphens (-), and underscores (_) and must not start with a space.                                                                                                           |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | The value can contain 1 to 64 characters.                                                                                                                                                                                       |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | uri             | Yes             | String          | Path of a custom automation script. Set this parameter to an OBS bucket path or a local VM path.                                                                                                                                |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | -  OBS bucket path: Enter a script path manually. for example, **s3a://**\ *XXX*\ **/scale.sh**.                                                                                                                                |
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

.. _mrs_02_0101__t4c9e3e169631470d81d260543affb7e1:

.. table:: **Table 13** **rules** parameter description

   +--------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+
   | Parameter          | Mandatory       | Type            | Description                                                                                                                    |
   +====================+=================+=================+================================================================================================================================+
   | name               | Yes             | String          | Name of an auto scaling rule.                                                                                                  |
   |                    |                 |                 |                                                                                                                                |
   |                    |                 |                 | A cluster name can contain only 1 to 64 characters. Only letters, digits, hyphens (-), and underscores (_) are allowed.        |
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
   | trigger            | Yes             | Trigger         | Condition for triggering a rule. For details, see :ref:`Table 14 <mrs_02_0101__t03bd10dc0ec94a3babc71b2d5d57c3fe>`.            |
   +--------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0101__t03bd10dc0ec94a3babc71b2d5d57c3fe:

.. table:: **Table 14** **trigger** parameter description

   +---------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter           | Mandatory       | Type            | Description                                                                                                                                                                                                       |
   +=====================+=================+=================+===================================================================================================================================================================================================================+
   | metric_name         | Yes             | String          | Metric name.                                                                                                                                                                                                      |
   |                     |                 |                 |                                                                                                                                                                                                                   |
   |                     |                 |                 | This triggering condition makes a judgment according to the value of the metric.                                                                                                                                  |
   |                     |                 |                 |                                                                                                                                                                                                                   |
   |                     |                 |                 | A metric name contains a maximum of 64 characters.                                                                                                                                                                |
   |                     |                 |                 |                                                                                                                                                                                                                   |
   |                     |                 |                 | :ref:`Table 15 <mrs_02_0101__t27de3279a99a48968dacb015c498d9cb>` lists the supported metric names.                                                                                                                |
   +---------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | metric_value        | Yes             | String          | Metric threshold to trigger a rule                                                                                                                                                                                |
   |                     |                 |                 |                                                                                                                                                                                                                   |
   |                     |                 |                 | The parameter value must be an integer or number with two decimal places only. :ref:`Table 15 <mrs_02_0101__t27de3279a99a48968dacb015c498d9cb>` provides value types and ranges corresponding to **metric_name**. |
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

.. _mrs_02_0101__t27de3279a99a48968dacb015c498d9cb:

.. table:: **Table 15** Auto scaling metrics

   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   | Cluster Type      | Metric                                   | Value Type      | Description                                                                                                  |
   +===================+==========================================+=================+==============================================================================================================+
   | Streaming cluster | StormSlotAvailable                       | Integer         | Number of available Storm slots.                                                                             |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSlotAvailablePercentage             | Percentage      | Percentage of available Storm slots, that is, the proportion of the available slots to total slots.          |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100.                                                                                       |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSlotUsed                            | Integer         | Number of the used Storm slots.                                                                              |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSlotUsedPercentage                  | Percentage      | Percentage of the used Storm slots, that is, the proportion of the used slots to total slots.                |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100.                                                                                       |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSupervisorMemAverageUsage           | Integer         | Average memory usage of the Supervisor process of Storm.                                                     |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSupervisorMemAverageUsagePercentage | Percentage      | Average percentage of the used memory of the Supervisor process of Storm to the total memory of the system.  |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100.                                                                                       |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSupervisorCPUAverageUsagePercentage | Percentage      | Average percentage of the used CPUs of the Supervisor process of Storm to the total CPUs.                    |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 6000.                                                                                      |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   | Analysis cluster  | YARNAppPending                           | Integer         | Number of pending tasks on Yarn.                                                                             |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNAppPendingRatio                      | Ratio           | Ratio of pending tasks on Yarn, that is, the ratio of pending tasks to running tasks on Yarn.                |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNAppRunning                           | Integer         | Number of running tasks on Yarn.                                                                             |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNContainerAllocated                   | Integer         | Number of containers allocated to Yarn.                                                                      |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNContainerPending                     | Integer         | Number of pending containers on Yarn.                                                                        |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNContainerPendingRatio                | Ratio           | Ratio of pending containers on Yarn, that is, the ratio of pending containers to running containers on Yarn. |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNCPUAllocated                         | Integer         | Number of virtual CPUs (vCPUs) allocated to Yarn                                                             |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNCPUAvailable                         | Integer         | Number of available vCPUs on Yarn.                                                                           |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNCPUAvailablePercentage               | Percentage      | Percentage of available vCPUs on Yarn, that is, the proportion of available vCPUs to total vCPUs.            |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100.                                                                                       |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNCPUPending                           | Integer         | Number of pending vCPUs on Yarn.                                                                             |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNMemoryAllocated                      | Integer         | Memory allocated to Yarn. The unit is MB.                                                                    |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNMemoryAvailable                      | Integer         | Available memory on Yarn. The unit is MB.                                                                    |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNMemoryAvailablePercentage            | Percentage      | Percentage of available memory on Yarn, that is, the proportion of available memory to total memory on Yarn. |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100.                                                                                       |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNMemoryPending                        | Integer         | Pending memory on Yarn.                                                                                      |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+

.. note::

   When the value type is percentage or ratio in :ref:`Table 15 <mrs_02_0101__t27de3279a99a48968dacb015c498d9cb>`, the valid value can be accurate to percentile. The percentage metric value is a decimal value with a percent sign (%) removed. For example, 16.80 represents 16.80%.

Response message.
-----------------

.. table:: **Table 16** Response parameters

   +------------+--------+---------------------------------------------------------------------------+
   | Parameter  | Type   | Description                                                               |
   +============+========+===========================================================================+
   | cluster_id | String | Cluster ID, which is returned by the system after the cluster is created. |
   +------------+--------+---------------------------------------------------------------------------+

Examples
--------

-  Request example

   -  Creating an Analysis Cluster

      .. code-block::

         {
           "cluster_version": "MRS 3.X.X",
           "cluster_name": "mrs_DyJA_dm",
           "cluster_type": "ANALYSIS",
           "charge_info": {
               "charge_mode": "postPaid"
           },
           "region": "",
           "availability_zone": "",
           "vpc_name": "vpc-37cd",
           "subnet_name": "subnet-ed99",
           "components": "Hadoop,Spark2x,HBase,Hive,Hue,Loader,Flink,Oozie,Ranger,Tez",
           "safe_mode": "KERBEROS",
           "manager_admin_password": "Mrs@1234",
           "login_mode": "PASSWORD",
           "node_root_password": "Mrs@1234",
           "log_collection": 1,
           "mrs_ecs_default_agency": "MRS_ECS_DEFAULT_AGENCY",
           "tags": [
             {
               "key": "tag1",
               "value": "111"
             },
             {
               "key": "tag2",
               "value": "222"
             }
           ],
           "node_groups": [
             {
               "group_name": "master_node_default_group",
               "node_num": 2,
               "node_size": "rc3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 600
               },
               "data_volume_count": 1
             },
            {
               "group_name": "core_node_analysis_group",
               "node_num": 3,
               "node_size": "rc3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 600
               },
               "data_volume_count": 1
             },
             {
               "group_name": "task_node_analysis_group",
               "node_num": 3,
               "node_size": "rc3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 600
               },
               "data_volume_count": 1,
              "auto_scaling_policy": {
                         "auto_scaling_enable": true,
                         "min_capacity": 0,
                         "max_capacity": 1,
                         "resources_plans": [],
                         "exec_scripts": [],
                         "rules": [
                             {
                                 "name": "default-expand-1",
                                 "description": "",
                                 "adjustment_type": "scale_out",
                                 "cool_down_minutes": 5,
                                 "scaling_adjustment": "1",
                                 "trigger": {
                                     "metric_id": 2003,
                                     "metric_name": "StormSlotAvailablePercentage",
                                     "metric_value": 100,
                                     "comparison_operator_id": 2003,
                                     "comparison_operator": "LTOE",
                                     "evaluation_periods": "1"
                                 }
                             }
                         ]
                     }
             }
           ]
         }

   -  Creating a Streaming Cluster

      .. code-block::

         {
           "cluster_version": "MRS 3.X.X",
           "cluster_name": "mrs_Dokle_dm",
           "cluster_type": "STREAMING",
           "charge_info": {
               "charge_mode": "postPaid"
           },
           "region": "",
           "availability_zone": "",
           "vpc_name": "vpc-37cd",
           "subnet_name": "subnet-ed99",
           "components": "Storm,Kafka,Flume,Ranger",
           "safe_mode": "KERBEROS",
           "manager_admin_password": "Mrs@1234",
           "login_mode": "PASSWORD",
           "node_root_password": "Mrs@1234",
           "log_collection": 1,
           "mrs_ecs_default_agency": "MRS_ECS_DEFAULT_AGENCY",
           "tags": [
             {
               "key": "tag1",
               "value": "111"
             },
             {
               "key": "tag2",
               "value": "222"
             }
           ],
           "node_groups": [
             {
               "group_name": "master_node_default_group",
               "node_num": 2,
               "node_size": "rc3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 300
               },
               "data_volume_count": 1
             },
             {
               "group_name": "core_node_streaming_group",
               "node_num": 3,
               "node_size": "rc3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 300
               },
               "data_volume_count": 1,
             },
             {
               "group_name": "task_node_streaming_group",
               "node_num": 0,
               "node_size": "rc3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 300
               },
               "data_volume_count": 1,
              "auto_scaling_policy": {
                         "auto_scaling_enable": true,
                         "min_capacity": 0,
                         "max_capacity": 1,
                         "resources_plans": [],
                         "exec_scripts": [],
                         "rules": [
                             {
                                 "name": "default-expand-1",
                                 "description": "",
                                 "adjustment_type": "scale_out",
                                 "cool_down_minutes": 5,
                                 "scaling_adjustment": "1",
                                 "trigger": {
                                     "metric_id": 2003,
                                     "metric_name": "StormSlotAvailablePercentage",
                                     "metric_value": 100,
                                     "comparison_operator_id": 2003,
                                     "comparison_operator": "LTOE",
                                     "evaluation_periods": "1"
                                 }
                             }
                         ]
                     }
              }
           ]
         }

   -  Creating a Hybrid Cluster

      .. code-block::

         {
           "cluster_version": "MRS 3.X.X",
           "cluster_name": "mrs_onmm_dm",
           "cluster_type": "MIXED",
           "charge_info": {
               "charge_mode": "postPaid"
           },
           "region": "",
           "availability_zone": "",
           "vpc_name": "vpc-37cd",
           "subnet_name": "subnet-ed99",
           "components": "Hadoop,Spark2x,HBase,Hive,Hue,Loader,Kafka,Storm,Flume,Flink,Oozie,Ranger,Tez",
           "safe_mode": "KERBEROS",
           "manager_admin_password": "Mrs@1234",
           "login_mode": "PASSWORD",
           "node_root_password": "Mrs@1234",
           "log_collection": 1,
           "mrs_ecs_default_agency": "MRS_ECS_DEFAULT_AGENCY",
           "tags": [
             {
               "key": "tag1",
               "value": "111"
             },
             {
               "key": "tag2",
               "value": "222"
             }
           ],
           "node_groups": [
             {
               "group_name": "master_node_default_group",
               "node_num": 2,
               "node_size": "Sit3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 300
               },
               "data_volume_count": 1
             },
             {
               "group_name": "core_node_streaming_group",
               "node_num": 3,
               "node_size": "Sit3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 300
               },
               "data_volume_count": 1
             },
             {
               "group_name": "core_node_analysis_group",
               "node_num": 3,
               "node_size": "Sit3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 300
               },
               "data_volume_count": 1,
             },
             {
               "group_name": "task_node_analysis_group",
               "node_num": 1,
               "node_size": "Sit3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 300
               },
               "data_volume_count": 1
             },
             {
               "group_name": "task_node_streaming_group",
               "node_num": 0,
               "node_size": "Sit3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 300
               },
               "data_volume_count": 1
             }
           ]
         }

   -  Creating a Customized Cluster with Co-deployed Management and Control Nodes

      .. code-block::

         {
           "cluster_version": "MRS 3.X.X",
           "cluster_name": "mrs_heshe_dm",
           "cluster_type": "CUSTOM",
           "charge_info": {
               "charge_mode": "postPaid"
           },
           "region": "",
           "availability_zone": "",
           "vpc_name": "vpc-37cd",
           "subnet_name": "subnet-ed99",
           "components": "Hadoop,Spark2x,HBase,Hive,Hue,Loader,Kafka,Storm,Flume,Flink,Oozie,Ranger,Tez",
           "safe_mode": "KERBEROS",
           "manager_admin_password": "Mrs@1234",
           "login_mode": "PASSWORD",
           "node_root_password": "Mrs@1234",
           "mrs_ecs_default_agency": "MRS_ECS_DEFAULT_AGENCY",
           "template_id": "mgmt_control_combined_v2",
           "log_collection": 1,
           "tags": [
             {
               "key": "tag1",
               "value": "111"
             },
             {
               "key": "tag2",
               "value": "222"
             }
           ],
           "node_groups": [
             {
               "group_name": "master_node_default_group",
               "node_num": 3,
               "node_size": "Sit3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 300
               },
               "data_volume_count": 1,
               "assigned_roles": [
                         "OMSServer:1,2",
                         "SlapdServer:1,2",
                         "KerberosServer:1,2",
                         "KerberosAdmin:1,2",
                         "quorumpeer:1,2,3",
                         "NameNode:2,3",
                         "Zkfc:2,3",
                         "JournalNode:1,2,3",
                         "ResourceManager:2,3",
                         "JobHistoryServer:2,3",
                         "DBServer:1,3",
                         "Hue:1,3",
                         "LoaderServer:1,3",
                         "MetaStore:1,2,3",
                         "WebHCat:1,2,3",
                         "HiveServer:1,2,3",
                         "HMaster:2,3",
                         "MonitorServer:1,2",
                         "Nimbus:1,2",
                         "UI:1,2",
                         "JDBCServer2x:1,2,3",
                         "JobHistory2x:2,3",
                         "SparkResource2x:1,2,3",
                         "oozie:2,3",
                         "LoadBalancer:2,3",
                         "TezUI:1,3",
                         "TimelineServer:3",
                         "RangerAdmin:1,2",
                         "UserSync:2",
                         "TagSync:2",
                         "KerberosClient",
                         "SlapdClient",
                         "meta",
                         "HSConsole:2,3",
                         "FlinkResource:1,2,3",
                         "DataNode:1,2,3",
                         "NodeManager:1,2,3",
                         "IndexServer2x:1,2",
                         "ThriftServer:1,2,3",
                         "RegionServer:1,2,3",
                         "ThriftServer1:1,2,3",
                         "RESTServer:1,2,3",
                         "Broker:1,2,3",
                         "Supervisor:1,2,3",
                         "Logviewer:1,2,3",
                         "Flume:1,2,3",
                         "HSBroker:1,2,3"
         ]
             },
             {
               "group_name": "node_group_1",
               "node_num": 3,
               "node_size": "Sit3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 300
               },
               "data_volume_count": 1,
               "assigned_roles": [
                         "DataNode",
                         "NodeManager",
                         "RegionServer",
                         "Flume:1",
                         "Broker",
                         "Supervisor",
                         "Logviewer",
                         "HBaseIndexer",
                         "KerberosClient",
                         "SlapdClient",
                         "meta",
                         "HSBroker:1,2",
                         "ThriftServer",
                         "ThriftServer1",
                         "RESTServer",
                         "FlinkResource"]
             },
             {
               "group_name": "node_group_2",
               "node_num": 1,
               "node_size": "Sit3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 300
               },
               "data_volume_count": 1,
               "assigned_roles": [
                         "NodeManager",
                         "KerberosClient",
                         "SlapdClient",
                         "meta",
                         "FlinkResource"]
             }
           ]
         }

   -  Creating a Cluster with Customized Management and Control Planes Deployed Separately

      .. code-block::

         {
           "cluster_version": "MRS 3.X.X",
           "cluster_name": "mrs_jdRU_dm01",
           "cluster_type": "CUSTOM",
           "charge_info": {
               "charge_mode": "postPaid"
           },
           "region": "",
           "availability_zone": "",
           "vpc_name": "vpc-37cd",
           "subnet_name": "subnet-ed99",
           "components": "Hadoop,Spark2x,HBase,Hive,Hue,Loader,Kafka,Storm,Flume,Flink,Oozie,Ranger,Tez",
           "safe_mode": "KERBEROS",
           "manager_admin_password": "Mrs@1234",
           "login_mode": "PASSWORD",
           "node_root_password": "Mrs@1234",
           "mrs_ecs_default_agency": "MRS_ECS_DEFAULT_AGENCY",
           "log_collection": 1,
           "template_id": "mgmt_control_separated_v2",
           "tags": [
             {
               "key": "aaa",
               "value": "111"
             },
             {
               "key": "bbb",
               "value": "222"
             }
           ],
           "node_groups": [
             {
               "group_name": "master_node_default_group",
               "node_num": 5,
               "node_size": "rc3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 300
               },
               "data_volume_count": 1,
               "assigned_roles": [
                         "OMSServer:1,2",
                         "SlapdServer:3,4",
                         "KerberosServer:3,4",
                         "KerberosAdmin:3,4",
                         "quorumpeer:3,4,5",
                         "NameNode:4,5",
                         "Zkfc:4,5",
                         "JournalNode:1,2,3,4,5",
                         "ResourceManager:4,5",
                         "JobHistoryServer:4,5",
                         "DBServer:3,5",
                         "Hue:1,2",
                         "LoaderServer:1,2",
                         "MetaStore:1,2,3,4,5",
                         "WebHCat:1,2,3,4,5",
                         "HiveServer:1,2,3,4,5",
                         "HMaster:4,5",
                         "MonitorServer:1,2",
                         "Nimbus:1,2",
                         "UI:1,2",
                         "JDBCServer2x:1,2,3,4,5",
                         "JobHistory2x:4,5",
                         "SparkResource2x:1,2,3,4,5",
                         "oozie:1,2",
                         "LoadBalancer:1,2",
                         "TezUI:1,2",
                         "TimelineServer:5",
                         "RangerAdmin:1,2",
                         "KerberosClient",
                         "SlapdClient",
                         "meta",
                         "HSConsole:1,2",
                         "FlinkResource:1,2,3,4,5",
                         "DataNode:1,2,3,4,5",
                         "NodeManager:1,2,3,4,5",
                         "IndexServer2x:1,2",
                         "ThriftServer:1,2,3,4,5",
                         "RegionServer:1,2,3,4,5",
                         "ThriftServer1:1,2,3,4,5",
                         "RESTServer:1,2,3,4,5",
                         "Broker:1,2,3,4,5",
                         "Supervisor:1,2,3,4,5",
                         "Logviewer:1,2,3,4,5",
                         "Flume:1,2,3,4,5",
                         "HBaseIndexer:1,2,3,4,5",
                         "TagSync:1",
                         "UserSync:1"]
             },
             {
               "group_name": "node_group_1",
               "node_num": 3,
               "node_size": "rc3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 300
               },
               "data_volume_count": 1,
               "assigned_roles": [
                         "DataNode",
                         "NodeManager",
                         "RegionServer",
                         "Flume:1",
                         "Broker",
                         "Supervisor",
                         "Logviewer",
                         "HBaseIndexer",
                         "KerberosClient",
                         "SlapdClient",
                         "meta",
                         "HSBroker:1,2",
                         "ThriftServer",
                         "ThriftServer1",
                         "RESTServer",
                         "FlinkResource"]
             }
           ]
         }

   -  Creating a User-Defined Data Cluster

      .. code-block::

         {
           "cluster_version": "MRS 3.X.X",
           "cluster_name": "mrs_jdRU_dm02",
           "cluster_type": "CUSTOM",
           "charge_info": {
               "charge_mode": "postPaid"
           },
           "region": "",
           "availability_zone": "",
           "vpc_name": "vpc-37cd",
           "subnet_name": "subnet-ed99",
           "components": "Hadoop,Spark2x,HBase,Hive,Hue,Loader,Kafka,Storm,Flume,Flink,Oozie,Ranger,Tez",
           "safe_mode": "KERBEROS",
           "manager_admin_password": "Mrs@1234",
           "login_mode": "PASSWORD",
           "node_root_password": "Mrs@1234",
           "mrs_ecs_default_agency": "MRS_ECS_DEFAULT_AGENCY",
           "template_id": "mgmt_control_data_separated_v2",
           "log_collection": 1,
           "tags": [
             {
               "key": "aaa",
               "value": "111"
             },
             {
               "key": "bbb",
               "value": "222"
             }
           ],
           "node_groups": [
             {
               "group_name": "master_node_default_group",
               "node_num": 9,
               "node_size": "rc3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 600
               },
               "data_volume_count": 1,
               "assigned_roles": [
                         "OMSServer:1,2",
                         "SlapdServer:5,6",
                         "KerberosServer:5,6",
                         "KerberosAdmin:5,6",
                         "quorumpeer:5,6,7,8,9",
                         "NameNode:3,4",
                         "Zkfc:3,4",
                         "JournalNode:5,6,7",
                         "ResourceManager:8,9",
                         "JobHistoryServer:8",
                         "DBServer:8,9",
                         "Hue:8,9",
                         "FlinkResource:3,4",
                         "LoaderServer:3,5",
                         "MetaStore:8,9",
                         "WebHCat:5",
                         "HiveServer:8,9",
                         "HMaster:8,9",
                         "FTP-Server:3,4",
                         "MonitorServer:3,4",
                         "Nimbus:8,9",
                         "UI:8,9",
                         "JDBCServer2x:8,9",
                         "JobHistory2x:8,9",
                         "SparkResource2x:5,6,7",
                         "oozie:4,5",
                         "EsMaster:7,8,9",
                         "LoadBalancer:8,9",
                         "TezUI:5,6",
                         "TimelineServer:5",
                         "RangerAdmin:4,5",
                         "UserSync:5",
                         "TagSync:5",
                         "KerberosClient",
                         "SlapdClient",
                         "meta",
                         "HSBroker:5",
                         "HSConsole:3,4",
                         "FlinkResource:3,4"]
             },
             {
               "group_name": "node_group_1",
               "node_num": 3,
               "node_size": "rc3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 600
               },
               "data_volume_count": 1,
               "assigned_roles": [
                         "DataNode",
                         "NodeManager",
                         "RegionServer",
                         "Flume:1",
                         "GraphServer",
                         "KerberosClient",
                         "SlapdClient",
                         "meta",
                         "HSBroker:1,2"
         ]
             },
             {
               "group_name": "node_group_2",
               "node_num": 3,
               "node_size": "rc3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 600
               },
               "data_volume_count": 1,
               "assigned_roles": [
                         "HBaseIndexer",
                         "SolrServer[3]",
                         "EsNode[2]",
                         "KerberosClient",
                         "SlapdClient",
                         "meta",
                         "SolrServerAdmin:1,2"]
             },
             {
               "group_name": "node_group_3",
               "node_num": 3,
               "node_size": "rc3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 600
               },
               "data_volume_count": 1,
               "assigned_roles": [
                         "Redis[2]",
                         "KerberosClient",
                         "SlapdClient",
                         "meta"]
             },
             {
               "group_name": "node_group_4",
               "node_num": 3,
               "node_size": "rc3.4xlarge.4.linux.bigdata",
               "root_volume": {
                 "type": "SAS",
                 "size": 100
               },
               "data_volume": {
                 "type": "SAS",
                 "size": 600
               },
               "data_volume_count": 1,
               "assigned_roles": [
                         "Broker",
                         "Supervisor",
                         "Logviewer",
                         "KerberosClient",
                         "SlapdClient",
                         "meta"]
             }
           ]
         }

-  Example response

   -  Example of a normal response

      .. code-block::

         {
             "cluster_id": "da1592c2-bb7e-468d-9ac9-83246e95447a"
         }

   -  Failed sample response

      .. code-block::

         {
             "error_code": "MRS.0002",
             "error_msg": "The parameter is invalid."
         }

Status Code
-----------

:ref:`Table 17 <mrs_02_0101__table1584477916050>` describes the status code of this API.

.. _mrs_02_0101__table1584477916050:

.. table:: **Table 17** Status Code

   =========== ==================================
   Status Code Description
   =========== ==================================
   200         A cluster is created successfully.
   =========== ==================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
