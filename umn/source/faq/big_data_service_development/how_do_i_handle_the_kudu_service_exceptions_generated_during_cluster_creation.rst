:original_name: mrs_03_1169.html

.. _mrs_03_1169:

How Do I Handle the Kudu Service Exceptions Generated During Cluster Creation?
==============================================================================

Viewing the Kudu Service Exception Logs
---------------------------------------

#. Log in to the MRS console.

#. Click the name of the cluster.

#. On the page displayed, choose **Components** > **Kudu** > **Instances** and locate the IP address of the abnormal instance.

   If the **Components** tab is unavailable, complete IAM user synchronization first. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

#. Log in to the node where the abnormal instance resides, and view the Kudu log.

   .. code-block:: console

      cd /var/log/Bigdata/Kudu
      [root@node-master1AERu kudu]# ls
      healthchecklog  runninglog  startlog

   You can find the Kudu health check logs in the **healthchecklog** directory, the startup logs in the **startlog** directory, and the Kudu process run logs in the **runninglog** directory.

   .. code-block:: console

      [root@node-master1AERu logs]# pwd
      /var/log/Bigdata/kudu/runninglog/master/logs
      [root@node-master1AERu logs]# ls -al
      kudu-master.ERROR   kudu-master.INFO   kudu-master.WARNING

   Run logs are classified into three types: ERROR, INFO, and WARNING. Each type of run logs is recorded in the corresponding file. You can run the **cat** command to view run logs of each type.

Handling Kudu Service Exceptions
--------------------------------

The **/var/log/Bigdata/kudu/runninglog/master/logs/kudu-master.INFO** file contains the following error information:

.. code-block::

   "Unable to init master catalog manager: not found: Unable to initialize catalog manager: Failed to initialize sys tables async: Unable to load consensus metadata for tablet 0000000000000000000000: xxx"

If this exception occurs when the Kudu service is installed for the first time, the KuduMaster service is not started. The data inconsistency causes the startup failure. To solve the problem, perform the following steps to clear the data directories and restart the Kudu service. If the Kudu service is not installed for the first time, clearing the data directories will cause data loss. In this case, migrate data and clear the data directory.

#. Search for the data directories **fs_data_dir**, **fs_wal_dir**, and **fs_meta_dir**.

   **find /opt -name master.gflagfile**

   **cat /opt/Bigdata/FusionInsight_Kudu_*/*_KuduMaster/etc/master.gflagfile \| grep fs\_**

#. On the cluster details page, choose **Components** > **Kudu** and click **Stop Service**.

#. Clear the Kudu data directories on all KuduMaster and KuduTserver nodes. The following command uses two data disks as an example.

   **rm -Rvf /srv/Bigdata/data1/kudu, rm -Rvf /srv/Bigdata/data2/kudu**

#. On the cluster details page, choose **Components** > **Kudu** and choose **More** > **Restart Service**.

#. Check the Kudu service status and logs.
