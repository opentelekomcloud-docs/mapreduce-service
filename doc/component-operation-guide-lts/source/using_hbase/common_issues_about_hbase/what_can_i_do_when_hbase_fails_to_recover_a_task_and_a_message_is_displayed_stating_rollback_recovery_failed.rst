:original_name: mrs_01_1659.html

.. _mrs_01_1659:

What Can I Do When HBase Fails to Recover a Task and a Message Is Displayed Stating "Rollback recovery failed"?
===============================================================================================================

Question
--------

The system automatically rolls back data after an HBase recovery task fails. If "Rollback recovery failed" is displayed, the rollback fails. After the rollback fails, data stops being processed and the junk data may be generated. How can I resolve this problem?

Answer
------

You need to manually clear the junk data before performing the backup or recovery task next time.

#. Install the cluster client in **/opt/client**.

#. Run **source /opt/client/bigdata_env** as the client installation user to configure the environment variable.

#. Run **kinit admin**.

#. Run **zkCli.sh -server** *business IP address of ZooKeeper*\ **:2181** to connect to the ZooKeeper.

#. Run **deleteall /recovering** to delete the junk data. Run **quit** to disconnect ZooKeeper.

   .. note::

      Running this command will cause data loss. Exercise caution.

#. Run **hdfs dfs -rm -f -r /user/hbase/backup** to delete temporary data.

#. On Manager, view related snapshot name information from recovery task records.

   .. code-block::

      Snapshot [ snapshot name ] is created successfully before recovery.

#. Switch to the client, run **hbase shell**, and then **delete_all_snapshot** '*snapshot name*\ **.*'** to delete the temporary snapshot.
