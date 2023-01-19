:original_name: mrs_01_1654.html

.. _mrs_01_1654:

Why HMaster Times Out While Waiting for Namespace Table to be Assigned After Rebuilding Meta Using OfflineMetaRepair Tool and Startups Failed
=============================================================================================================================================

Question
--------

Why HMaster times out while waiting for namespace table to be assigned after rebuilding meta using OfflineMetaRepair tool and startups failed?

HMaster abort with following FATAL message,

.. code-block::

   2017-06-15 15:11:07,582 FATAL [Hostname:16000.activeMasterManager] master.HMaster: Unhandled exception. Starting shutdown.
   java.io.IOException: Timedout 120000ms waiting for namespace table to be assigned
           at org.apache.hadoop.hbase.master.TableNamespaceManager.start(TableNamespaceManager.java:98)
           at org.apache.hadoop.hbase.master.HMaster.initNamespace(HMaster.java:1054)
           at org.apache.hadoop.hbase.master.HMaster.finishActiveMasterInitialization(HMaster.java:848)
           at org.apache.hadoop.hbase.master.HMaster.access$600(HMaster.java:199)
           at org.apache.hadoop.hbase.master.HMaster$2.run(HMaster.java:1871)
           at java.lang.Thread.run(Thread.java:745)

Answer
------

When meta is rebuilt by OfflineMetaRepair tool then HMaster wait for all region server's WAL split during start up to avoid the data inconsistency problem. HMaster trigger user regions assignment once WAL split completes. So when the cluster is in the unusual scenario, there are chances WAL splitting may take long time which depends on multiple factors like too many WALs, slow I/O, region servers are not stable etc.

HMaster should be able to finish all region server WAL splitting successfully. Perform the following steps.

#. Make sure cluster is stable, no other problem exist. If any problem occurs, please correct them first.
#. Configure a large value to **hbase.master.initializationmonitor.timeout** parameters, default value is **3600000** milliseconds.
#. Restart HBase service.
