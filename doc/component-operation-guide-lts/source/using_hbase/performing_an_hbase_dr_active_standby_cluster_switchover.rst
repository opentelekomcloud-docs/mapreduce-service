:original_name: mrs_01_1611.html

.. _mrs_01_1611:

Performing an HBase DR Active/Standby Cluster Switchover
========================================================

Scenario
--------

The HBase cluster in the current environment is a DR cluster. Due to some reasons, the active and standby clusters need to be switched over. That is, the standby cluster becomes the active cluster, and the active cluster becomes the standby cluster.

Impact on the System
--------------------

After the active and standby clusters are switched over, data cannot be written to the original active cluster, and the original standby cluster becomes the active cluster to take over upper-layer services.

Procedure
---------

**Ensuring that upper-layer services are stopped**

#. Ensure that the upper-layer services have been stopped. If not, perform operations by referring to :ref:`Performing an HBase DR Service Switchover <mrs_01_1610>`.

**Disabling the write function of the active cluster**

2. Download and install the HBase client.

3. On the HBase client of the standby cluster, run the following command as user **hbase** to disable the data write function of the standby cluster:

   **kinit hbase**

   **hbase shell**

   **set_clusterState_standby**

   The command is run successfully if the following information is displayed:

   .. code-block::

      hbase(main):001:0> set_clusterState_standby
      => true

**Checking whether the active/standby synchronization is complete**

4. Run the following command to ensure that the current data has been synchronized (SizeOfLogQueue=0 and SizeOfLogToReplicate=0 are required). If the values are not 0, wait and run the following command repeatedly until the values are 0.

   **status 'replication'**

**Disabling synchronization between the active and standby clusters**

5. Query all synchronization clusters and obtain the value of **PEER_ID**.

   **list_peers**

6. Delete all synchronization clusters.

   **remove_peer** *'Standby cluster ID'*

   Example:

   **remove_peer** **'**\ *\ 1\ *\ **'**

7. Query all synchronized tables.

   **list_replicated_tables**

8. Disable all synchronized tables queried in the preceding step.

   **disable_table_replication** *'Table name'*

   Example:

   **disable_table_replication** *'t1'*

**Performing an active/standby switchover**

9. Reconfigure HBase DR. For details, see :ref:`Configuring HBase DR <mrs_01_1609>`.
