:original_name: mrs_01_1052.html

.. _mrs_01_1052:

Migrating Services of External Security Components Interconnected with Storm
============================================================================

Migrating Services for Interconnecting Storm with HDFS and HBase
----------------------------------------------------------------

If the Storm services use the **storm-hdfs** or **storm-hbase** plug-in package for interconnection, you need to specify the following security parameters when migrating Storm services as instructed in :ref:`Completely Migrating Storm Services <mrs_01_1050>`.

.. code-block::

   //Initialize Storm Config.
   Config conf = new Config();

   //Initialize the security plug-in list.
   List<String> auto_tgts = new ArrayList<String>();
   //Add the AutoTGT plug-in.
   auto_tgts.add("org.apache.storm.security.auth.kerberos.AutoTGT");
   //Add the AutoHDFS plug-in.
   //If HBase is interconnected, use auto_tgts.add("org.apache.storm.hbase.security.AutoHBase") to replace the following:
   auto_tgts.add("org.apache.storm.hdfs.common.security.AutoHDFS");

   //Set security parameters.
   conf.put(Config.TOPOLOGY_AUTO_CREDENTIALS, auto_tgts);
   //Set the number of workers.
   conf.setNumWorkers(3);

   //Convert Storm Config to StormConfig of Flink.
   StormConfig stormConfig = new StormConfig(conf);

   //Construct FlinkTopology using TopologBuilder of Storm.
   FlinkTopology topology = FlinkTopology.createTopology(builder);

   //Obtain the StreamExecutionEnvironment.
   StreamExecutionEnvironment env = topology.getExecutionEnvironment();

   //Add StormConfig to the environment variable of Job to construct Bolt and Spout.
   //If Config is not required during the initialization of Bolt and Spout, do not set this parameter.
   env.getConfig().setGlobalJobParameters(stormConfig);

   //Submit the topology.
   topology.execute();

After the preceding security plug-in is configured, unnecessary logins during the initialization of HDFSBolt and HBaseBolt are avoided because the security context has been configured in Flink.

Migrating Services of Storm Interconnected with Other Security Components
-------------------------------------------------------------------------

If the plug-in packages, such as **storm-kakfa-client** and **storm-solr** are used for interconnection between Storm and other components for service migration, the previously configured security plug-ins need to be deleted.

.. code-block::

   List<String> auto_tgts = new ArrayList<String>();
   //keytab mode
   auto_tgts.add("org.apache.storm.security.auth.kerberos.AutoTGTFromKeytab");

   //Write the plug-in list configured on the client to the specified config parameter.
   //Mandatory in security mode
   //This configuration is not required in common mode, and you can comment out the following line.
   conf.put(Config.TOPOLOGY_AUTO_CREDENTIALS, auto_tgts);

The AutoTGTFromKeytab plug-in must be deleted during service migration. Otherwise, the login will fail when Bolt or Spout is initialized.
