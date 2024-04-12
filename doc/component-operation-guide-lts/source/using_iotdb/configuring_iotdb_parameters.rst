:original_name: mrs_01_24159.html

.. _mrs_01_24159:

Configuring IoTDB Parameters
============================

Scenario
--------

IoTDB uses the multi-replica deployment architecture to implement cluster high availability. Each region (DataRegion and SchemaRegion) has three replicas by default. You can also configure more replicas. If a node is faulty, replicas on other nodes of the region replica can take over services from the faulty node, ensuring service continuity and improving cluster stability.

Procedure
---------

#. Log in to Manager, choose **Cluster** > **Services** > **IoTDB** > **Configurations** > **All Configurations** to go to the IoTDB configuration page, and modify the parameters.

#. Modify the ConfigNode and IoTDBServer configurations.

   -  Modifying the ConfigNode configuration:

      -  Click **ConfigNode(Role)**. You can modify the existing configuration according to :ref:`Table 1 <mrs_01_24159__table3406106165317>`.
      -  Choose **ConfigNode(Role)** > **Customization**. You can customize ConfigNode configurations in the **confignode.customized.configs** parameter according to :ref:`Table 1 <mrs_01_24159__table3406106165317>`.

   -  Modifying the IoTDBServer configuration:

      -  Click **IoTDBServer(Role)**. You can modify the existing configuration according to :ref:`Table 1 <mrs_01_24159__table3406106165317>`.
      -  Choose **IoTDBServer(Role)** > **Customization**. You can customize IoTDBServer configurations in the **engine.customized.configs** parameter according to :ref:`Table 1 <mrs_01_24159__table3406106165317>`.

   .. _mrs_01_24159__table3406106165317:

   .. table:: **Table 1** Common parameters

      +--------------------------------+-------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                      | Role        | Example Value | Description                                                                                                                                    |
      +================================+=============+===============+================================================================================================================================================+
      | read_consistency_level         | ConfigNode  | strong        | Read consistency level of the custom parameter **confignode.customized.configs**. Currently, the value can only be **strong** or **weak**.     |
      +--------------------------------+-------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------+
      | flush_proportion               | IoTDBServer | 0.4           | Write memory ratio for invoking disk flushing. If the write load is too high (for example, batch processing = 1000), you can reduce the value. |
      +--------------------------------+-------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------+
      | replica_affinity_policy        | IoTDBServer | random        | When the value of **read_consistency_level** is **weak**, the strategy of the region replica node is selected for the query task.              |
      +--------------------------------+-------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------+
      | coordinator_read_executor_size | IoTDBServer | 20            | Number of read thread cores of the IoTDBServer Coordinator of the custom parameter **engine.customized.configs**                               |
      +--------------------------------+-------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------+
      | rpc_thrift_compression_enable  | ALL         | false         | Whether to compress data during transmission. Data is not compressed by default.                                                               |
      +--------------------------------+-------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------+
      | root.log.level                 | ALL         | INFO          | IoTDB log level. The modification of this parameter takes effect without restarting related instances.                                         |
      +--------------------------------+-------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------+
      | SSL_ENABLE                     | ALL         | true          | Whether to encrypt the channel between the client and server using SSL                                                                         |
      +--------------------------------+-------------+---------------+------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Save**.

#. Click the **Instance** tab. Select the corresponding instance and choose **More** > **Restart Instance** to make the configuration take effect.
