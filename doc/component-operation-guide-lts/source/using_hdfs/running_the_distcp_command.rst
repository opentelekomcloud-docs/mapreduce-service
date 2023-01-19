:original_name: mrs_01_0794.html

.. _mrs_01_0794:

Running the DistCp Command
==========================

Scenario
--------

DistCp is a tool used to perform large-amount data replication between clusters or in a cluster. It uses MapReduce tasks to implement distributed copy of a large amount of data.

Prerequisites
-------------

-  The Yarn client or a client that contains Yarn has been installed. For example, the installation directory is **/opt/client**.
-  Service users of each component are created by the system administrator based on service requirements. In security mode, machine-machine users need to download the keytab file. A human-machine user must change the password upon the first login. (Not involved in normal mode)
-  To copy data between clusters, you need to enable the inter-cluster data copy function on both clusters.

Procedure
---------

#. Log in to the node where the client is installed.

#. Run the following command to go to the client installation directory:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If the cluster is in security mode, the user group to which the user executing the DistCp command belongs must be **supergroup** and the user run the following command to perform user authentication. In normal mode, user authentication is not required.

   **kinit** *Component service user*

#. Run the DistCp command. The following provides an example:

   **hadoop distcp hdfs://hacluster/source hdfs://hacluster/target**

Common Usage of DistCp
----------------------

#. The following is an example of the commonest usage of DistCp:

   .. code-block::

      hadoop distcp -numListstatusThreads 40 -update -delete -prbugpaxtq hdfs://cluster1/source hdfs://cluster2/target

   .. note::

      In the preceding command:

      -  **-numListstatusThreads** specifies the number of threads for creating the list of 40 copied files.

      -  **-update -delete** specifies that files at the source location and the target location are synchronized, and that files with excessive target locations are deleted. If you need to copy files incrementally, delete **-delete**.

      -  If **-prbugpaxtq** and **-update** are used, it indicates that the status information of the copied file is also updated.

      -  **hdfs://cluster1/source** indicates the source location, and **hdfs://cluster2/target** indicates the target location.

#. The following is an example of data copy between clusters:

   .. code-block::

      hadoop distcp hdfs://cluster1/foo/bar hdfs://cluster2/bar/foo

   .. note::

      The network between cluster1 and cluster2 must be reachable, and the two clusters must use the same HDFS version or compatible HDFS versions.

#. The following are multiple examples of data copy in a source directory:

   .. code-block::

      hadoop distcp hdfs://cluster1/foo/a \
      hdfs://cluster1/foo/b \
      hdfs://cluster2/bar/foo

   The preceding command is used to copy the folders a and b of cluster1 to the **/bar/foo** directory of cluster2. The effect is equivalent to that of the following commands:

   .. code-block::

      hadoop distcp -f hdfs://cluster1/srclist \
      hdfs://cluster2/bar/foo

   The content of **srclist** is as follows. Before running the DistCp command, upload the **srclist** file to HDFS.

   .. code-block::

      hdfs://cluster1/foo/a
      hdfs://cluster1/foo/b

#. **-update** indicates that a to-be-copied file does not exist in the target location, or the content of the copied file in the target location is updated; and **-overwrite** is used to overwrite existing files in the target location.

   The following is an example of the difference between no option and any one of the two options (either **update** or **overwrite**) that is added:

   Assume that the structure of a file at the source location is as follows:

   .. code-block::

      hdfs://cluster1/source/first/1
      hdfs://cluster1/source/first/2
      hdfs://cluster1/source/second/10
      hdfs://cluster1/source/second/20

   Commands without options are as follows:

   .. code-block::

      hadoop distcp hdfs://cluster1/source/first  hdfs://cluster1/source/second  hdfs://cluster2/target

   By default, the preceding command creates the **first** and **second** folders at the target location. Therefore, the copy results are as follows:

   .. code-block::

      hdfs://cluster2/target/first/1
      hdfs://cluster2/target/first/2
      hdfs://cluster2/target/second/10
      hdfs://cluster2/target/second/20

   The command with any one of the two options (for example, **update**) is as follows:

   .. code-block::

      hadoop distcp -update hdfs://cluster1/source/first  hdfs://cluster1/source/second  hdfs://cluster2/target

   The preceding command copies only the content at the source location to the target location. Therefore, the copy results are as follows:

   .. code-block::

      hdfs://cluster2/target/1
      hdfs://cluster2/target/2
      hdfs://cluster2/target/10
      hdfs://cluster2/target/20

   .. note::

      -  If files with the same name exist in multiple source locations, the DistCp command fails.

      -  If neither **update** nor **overwrite** is used and the file to be copied already exists in the target location, the file will be skipped.
      -  When **update** is used, if the file to be copied already exists in the target location but the file content is different, the file content in the target location is updated.
      -  When **overwrite** is used, if the file to be copied already exists in the target location, the file in the target location is still overwritten.

#. The following table describes other command options:

   .. table:: **Table 1** Other command options

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Option                            | Description                                                                                                                                                                                                                                                                                                  |
      +===================================+==============================================================================================================================================================================================================================================================================================================+
      | -p[rbugpcaxtq]                    | When **-update** is also used, the status information of a copied file is updated even if the content of the copied file is not updated.                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                                                                                                              |
      |                                   | **r**: number of copies                                                                                                                                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                                                                                                                              |
      |                                   | **b**: size of a block                                                                                                                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                                                                                              |
      |                                   | **u**: user to which the files belong                                                                                                                                                                                                                                                                        |
      |                                   |                                                                                                                                                                                                                                                                                                              |
      |                                   | **g**: user group to which the user belongs                                                                                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                                                                                              |
      |                                   | **p**: permission                                                                                                                                                                                                                                                                                            |
      |                                   |                                                                                                                                                                                                                                                                                                              |
      |                                   | **c**: check and type                                                                                                                                                                                                                                                                                        |
      |                                   |                                                                                                                                                                                                                                                                                                              |
      |                                   | **a**: access control                                                                                                                                                                                                                                                                                        |
      |                                   |                                                                                                                                                                                                                                                                                                              |
      |                                   | **t**: timestamp                                                                                                                                                                                                                                                                                             |
      |                                   |                                                                                                                                                                                                                                                                                                              |
      |                                   | **q**: quota information                                                                                                                                                                                                                                                                                     |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -i                                | Failures ignored during copying                                                                                                                                                                                                                                                                              |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -log <logdir>                     | Path of the specified log                                                                                                                                                                                                                                                                                    |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -v                                | Additional information in the specified log                                                                                                                                                                                                                                                                  |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -m <num_maps>                     | Maximum number of concurrent copy tasks that can be executed at the same time                                                                                                                                                                                                                                |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -numListstatusThreads             | Number of threads for constituting the list of copied files. This option increases the running speed of DistCp.                                                                                                                                                                                              |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -overwrite                        | File at the target location that is to be overwritten                                                                                                                                                                                                                                                        |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -update                           | A file at the target location is updated if the size and check of a file at the source location are different from those of the file at the target location.                                                                                                                                                 |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -append                           | When **-update** is also used, the content of the file at the source location is added to the file at the target location.                                                                                                                                                                                   |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -f <urilist_uri>                  | Content of the **<urilist_uri>** file is used as the file list to be copied.                                                                                                                                                                                                                                 |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -filters                          | A local file is specified whose content contains multiple regular expressions. If the file to be copied matches a regular expression, the file is not copied.                                                                                                                                                |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -async                            | The **distcp** command is run asynchronously.                                                                                                                                                                                                                                                                |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -atomic {-tmp <tmp_dir>}          | An atomic copy can be performed. You can add a temporary directory during copying.                                                                                                                                                                                                                           |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -bandwidth                        | The transmission bandwidth of each copy task. Unit: MB/s.                                                                                                                                                                                                                                                    |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -delete                           | The files that exist in the target location is deleted but do not exist in the source location. This option is usually used with **-update**, and indicates that files at the source location are synchronized with those at the target location and the redundant files at the target location are deleted. |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -diff <oldSnapshot> <newSnapshot> | The differences between the old and new versions are copied to a file in the old version at the target location.                                                                                                                                                                                             |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -skipcrccheck                     | Whether to skip the cyclic redundancy check (CRC) between the source file and the target file.                                                                                                                                                                                                               |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -strategy {dynamic|uniformsize}   | The policy for copying a task. The default policy is **uniformsize**, that is, each copy task copies the same number of bytes.                                                                                                                                                                               |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -preserveec                       | Whether to retain the erasure code (EC) policy.                                                                                                                                                                                                                                                              |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

FAQs of DistCp
--------------

#. When you run the DistCp command, if the content of some copied files is large, you are advised to change the timeout period of MapReduce that executes the copy task. It can be implemented by specifying the **mapreduce.task.timeout** in the DistCp command. For example, run the following command to change the timeout to 30 minutes:

   .. code-block::

      hadoop distcp -Dmapreduce.task.timeout=1800000 hdfs://cluster1/source hdfs://cluster2/target

   Or, you can also use **filters** to exclude the large files out of the copy process. The command example is as follows:

   .. code-block::

      hadoop distcp -filters /opt/client/filterfile hdfs://cluster1/source hdfs://cluster2/target

   In the preceding command, *filterfile* indicates a local file, which contains multiple expressions used to match the path of a file that is not copied. The following is an example:

   .. code-block::

      .*excludeFile1.*
      .*excludeFile2.*

#. If the DistCp command unexpectedly quits, the error message "java.lang.OutOfMemoryError" is displayed.

   This is because the memory required for running the copy command exceeds the preset memory limit (default value: 128 MB). You can change the memory upper limit of the client by modifying **CLIENT_GC_OPTS** in *<Client installation path>*\ **/HDFS/component_env**. For example, if you want to set the memory upper limit to 1 GB, refer to the following configuration:

   .. code-block::

      CLIENT_GC_OPTS="-Xmx1G"

   After the modification, run the following command to make the modification take effect:

   **source** {*Client installation path*}\ **/bigdata_env**

#. When the dynamic policy is used to run the DistCp command, the command exits unexpectedly and the error message "Too many chunks created with splitRatio" is displayed.

   The cause of this problem is that the value of **distcp.dynamic.max.chunks.tolerable** (default value: 20,000) is less than the value of **distcp.dynamic.split.ratio** (default value: 2) multiplied by the number of Maps. This problem occurs when the number of Maps exceeds 10,000. You can use the **-m** parameter to reduce the number of Maps to less than 10,000.

   .. code-block::

      hadoop distcp -strategy dynamic -m 9500 hdfs://cluster1/source hdfs://cluster2/target

   Alternatively, you can use the **-D** parameter to set **distcp.dynamic.max.chunks.tolerable** to a large value.

   .. code-block::

      hadoop distcp -Ddistcp.dynamic.max.chunks.tolerable=30000 -strategy dynamic hdfs://cluster1/source hdfs://cluster2/target
