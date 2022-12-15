:original_name: mrs_01_0757.html

.. _mrs_01_0757:

Common Operations of Alluxio
============================

Preparations
------------

#. Create a cluster with Alluxio installed.

#. Log in to the active Master node in a cluster as user **root** using the password set during cluster creation.

#. Run the following command to configure environment variables:

   **source /opt/client/bigdata_env**

Using the Alluxio Shell
-----------------------

The `Alluxio shell <https://docs.alluxio.io/os/user/2.0/en/basic/Command-Line-Interface.html>`__ contains multiple command line operations that interact with Alluxio.

-  View a file system operation command list:

   **alluxio fs**

-  Run the **ls** command to list the files in Alluxio. For example, list all files in the root directory:

   **alluxio fs ls /**

-  Run the **copyFromLocal** command to copy local files to Alluxio:

   **alluxio fs copyFromLocal /home/test_input.txt /test_input.txt**

   Command output:

   .. code-block::

      Copied file:///home/test_input.txt to /test_input.txt

-  Run the **ls** command again to list the files in Alluxio. The copied **test_input.txt** file is listed:

   **alluxio fs ls /**

   Command output:

   .. code-block::

      12       PERSISTED 11-28-2019 17:10:17:449 100% /test_input.txt

   The **test_input.txt** file is displayed in Alluxio. The parameters in the file indicate the file size, whether the file is persistent, creation date, cache ratio of the file in Alluxio, and file name.

-  Run the **cat** command to print file content:

   **alluxio fs cat /test_input.txt**

   Command output:

   .. code-block::

      Test Alluxio

Mounting Function of Alluxio
----------------------------

Alluxio uses a unified namespace feature to unify the access to storage systems. For details, see https://docs.alluxio.io/os/user/2.0/en/advanced/Namespace-Management.html.

This feature allows users to mount different storage systems to an Alluxio namespace and seamlessly access files across storage systems through the Alluxio namespace.

#. Create a directory as a mount point in Alluxio.

   **alluxio fs mkdir /mnt**

   .. code-block::

      Successfully created directory /mnt

#. Mount an existing OBS file system to Alluxio. (Prerequisite: An agency with the **OBS OperateAccess** permission has been configured for the cluster. The **obs-mrstest** file system is used as an example. Replace the file system name with the actual one.

   **alluxio fs mount /mnt/obs obs://obs-mrstest/data**

   .. code-block::

      Mounted obs://obs-mrstest/data at /mnt/obs

#. List files in the OBS file system using the Alluxio namespace. Run the **ls** command to list the files in the OBS mount directory.

   **alluxio fs ls /mnt/obs**

   .. code-block::

      38       PERSISTED 11-28-2019 17:42:54:554   0% /mnt/obs/hive_load.txt
      12       PERSISTED 11-28-2019 17:43:07:743   0% /mnt/obs/test_input.txt

   You can also view the newly mounted files and directories on the Alluxio web UI.

#. After the mounting is complete, you can seamlessly exchange data between different storage systems through the unified namespace of Alluxio. For example, run the **ls -R** command to list all files in a directory recursively:

   **alluxio fs ls -R /**

   .. code-block::

              0       PERSISTED 11-28-2019 11:15:19:719  DIR /app-logs
              1       PERSISTED 11-28-2019 11:18:36:885  DIR /apps
              1       PERSISTED 11-28-2019 11:18:40:209  DIR /apps/templeton
      239440292       PERSISTED 11-28-2019 11:18:40:209   0% /apps/templeton/hive.tar.gz
      .....
              1       PERSISTED 11-28-2019 19:00:23:879  DIR /mnt
              2       PERSISTED 11-28-2019 19:00:23:879  DIR /mnt/obs
             38       PERSISTED 11-28-2019 17:42:54:554   0% /mnt/obs/hive_load.txt
             12       PERSISTED 11-28-2019 17:43:07:743   0% /mnt/obs/test_input.txt
      .....

   The command output shows all files that are from the mounted storage system in the root directory of the Alluxio file system (the default directory is the HDFS root directory, that is, **hdfs://hacluster/**). The **/app-logs** and **/apps** directories are in HDFS, and the **/mnt/obs/** directory is in OBS.

Using Alluxio to Accelerate Data Access
---------------------------------------

Alluxio can accelerate data access, because it uses memory to store data. Example commands are provided as follows:

#. Upload the **test_data.csv** file (a sample that records recipes) to the **/data** directory of the **obs-mrstest** file system. Run the **ls** command to display the file status.

   **alluxio fs ls /mnt/obs/test_data.csv**

   .. code-block::

      294520189       PERSISTED 11-28-2019 19:38:55:000   0% /mnt/obs/test_data.csv

   The output indicates that the cache percentage of the file in Alluxio is 0%, that is, the file is not in Alluxio memory.

#. Count the occurrence times of the word "milk" in the file, and calculate the time consumed.

   **time alluxio fs cat /mnt/obs/test_data.csv \| grep -c milk**

   .. code-block::

      52180

      real    0m10.765s
      user    0m5.540s
      sys     0m0.696s

#. Data is stored in memory after being read for the first time. When Alluxio reads data again, the data access speed is increased. For example, after running the **cat** command to obtain a file, run the **ls** command to check the file status.

   **alluxio fs ls /mnt/obs/test_data.csv**

   .. code-block::

      294520189       PERSISTED 11-28-2019 19:38:55:000 100% /mnt/obs/test_data.csv

   The output shows that the file has been fully loaded to Alluxio.

#. Access the file again, count the occurrence times of the word "eggs", and calculate the time consumed.

   **time alluxio fs cat /mnt/obs/test_data.csv \| grep -c eggs**

   .. code-block::

      59510

      real    0m5.777s
      user    0m5.992s
      sys     0m0.592s

   According to the comparison of the two time consumption records, the time consumed for accessing data stored in Alluxio memory is significantly reduced.
