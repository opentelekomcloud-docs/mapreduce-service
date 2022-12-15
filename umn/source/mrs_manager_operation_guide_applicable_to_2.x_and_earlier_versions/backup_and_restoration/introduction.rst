:original_name: mrs_01_0551.html

.. _mrs_01_0551:

Introduction
============

Purpose
-------

MRS Manager provides backup and restoration for user data and system data. The backup function is provided based on components to back up Manager data (including OMS data and LdapServer data), Hive user data, component metadata saved in DBService, and HDFS metadata.

Backup and restoration tasks are performed in the following scenarios:

-  Routine backup is performed to ensure the data security of the system and components.
-  If the system is faulty, the data backup can be used to recover the system.
-  If the active cluster is completely faulty, a mirror cluster identical to the active cluster needs to be created. You can use the backup data to restore the active cluster.

.. table:: **Table 1** Backing up metadata

   +-------------+-------------------------------------------------------------------------------------------------------------------------+
   | Backup Type | Backup Content                                                                                                          |
   +=============+=========================================================================================================================+
   | OMS         | Database data (excluding alarm data) and configuration data in the cluster management system to be backed up by default |
   +-------------+-------------------------------------------------------------------------------------------------------------------------+
   | LdapServer  | User information, including the username, password, key, password policy, and group information                         |
   +-------------+-------------------------------------------------------------------------------------------------------------------------+
   | DBService   | Metadata of the components (Hive) managed by DBService                                                                  |
   +-------------+-------------------------------------------------------------------------------------------------------------------------+
   | NameNode    | HDFS metadata.                                                                                                          |
   +-------------+-------------------------------------------------------------------------------------------------------------------------+

Principles
----------

**Task**

Before backup or restoration, you need to create a backup or restoration task and set task parameters, such as the task name, backup data source, and type of backup file save path. Data backup and restoration can be performed by executing backup and restoration tasks. When the Manager is used to recover the data of HDFS, HBase, Hive, and NameNode, no cluster can be accessed.

Each backup task can back up data of different data sources and generates an independent backup file for each data source. All the backup files generated in each backup task form a backup file set, which can be used in restoration tasks. Backup data can be stored on Linux local disks, local cluster HDFS, and standby cluster HDFS. The backup task provides the full backup or incremental backup policies. HDFS and Hive backup tasks support the incremental backup policy, while OMS, LdapServer, DBService, and NameNode backup tasks support only the full backup policy.

.. note::

   Task execution rules:

   -  If a task is being executed, the task cannot be executed repeatedly and other tasks cannot be started at the same time.
   -  The interval at which a periodical task is automatically executed must be greater than 120s; otherwise, the task is postponed and will be executed in the next period. Manual tasks can be executed at any interval.
   -  When a periodic task is to be automatically executed, the current time cannot be 120s later than the task start time; otherwise, the task is postponed and executed in the next period.
   -  When a periodic task is locked, it cannot be automatically executed and needs to be manually unlocked.
   -  Before an OMS, LdapServer, DBService, or NameNode backup task starts, ensure that the LocalBackup partition on the active management node has more than 20 GB available space. Otherwise, the backup task cannot be started.
   -  When you are planning backup and restoration tasks, select the data to be backed up or restored strictly based on the service logic, data store structure, and database or table association. The system creates a default periodic backup task **default** whose execution interval is 24 hours to perform full backup of OMS, LdapServer, DBService, and NameNode data to the Linux local disk.

Specifications
--------------

.. table:: **Table 2** Backup and restoration feature specifications

   ======================================================= ==============
   Item                                                    Specifications
   ======================================================= ==============
   Maximum number of backup or restoration tasks           100
   Number of concurrent running tasks                      1
   Maximum number of waiting tasks                         199
   Maximum size of backup files on a Linux local disk (GB) 600
   ======================================================= ==============

.. table:: **Table 3** Specifications of the **default** task

   +---------------------------------+--------------------------------------------------------------------------------+------------+-----------+----------+
   | Item                            | OMS                                                                            | LdapServer | DBService | NameNode |
   +=================================+================================================================================+============+===========+==========+
   | Backup period                   | 1 hour                                                                         |            |           |          |
   +---------------------------------+--------------------------------------------------------------------------------+------------+-----------+----------+
   | Maximum number of copies        | 2                                                                              |            |           |          |
   +---------------------------------+--------------------------------------------------------------------------------+------------+-----------+----------+
   | Maximum size of a backup file   | 10 MB                                                                          | 20 MB      | 100 MB    | 1.5 GB   |
   +---------------------------------+--------------------------------------------------------------------------------+------------+-----------+----------+
   | Maximum size of disk space used | 20 MB                                                                          | 40 MB      | 200 MB    | 3 GB     |
   +---------------------------------+--------------------------------------------------------------------------------+------------+-----------+----------+
   | Save path of backup data        | *Data save path*\ **/LocalBackup/** of the active and standby management nodes |            |           |          |
   +---------------------------------+--------------------------------------------------------------------------------+------------+-----------+----------+

.. note::

   The backup data of the **default** task must be periodically transferred and saved outside the cluster based on the enterprise O&M requirements.
