:original_name: mrs_01_0799.html

.. _mrs_01_0799:

Planning HDFS Capacity
======================

In HDFS, DataNode stores user files and directories as blocks, and file objects are generated on the NameNode to map each file, directory, and block on the DataNode.

The file objects on the NameNode require certain memory capacity. The memory consumption linearly increases as more file objects generated. The number of file objects on the NameNode increases and the objects consume more memory when the files and directories stored on the DataNode increase. In this case, the existing hardware may not meet the service requirement and the cluster is difficult to be scaled out.

Capacity planning of the HDFS that stores a large number of files is to plan the capacity specifications of the NameNode and DataNode and to set parameters according to the capacity plans.

Capacity Specifications
-----------------------

-  NameNode capacity specifications

   Each file object on the NameNode corresponds to a file, directory, or block on the DataNode.

   A file uses at least one block. The default size of a block is **134,217,728**, that is, 128 MB, which can be set in the **dfs.blocksize** parameter. By default, a file whose size is less than 128 MB occupies only one block. If the file size is greater than 128 MB, the number of occupied blocks is the file size divided by 128 MB (Number of occupied blocks = File size/128). The directories do not occupy any blocks.

   Based on **dfs.blocksize**, the number of file objects on the NameNode is calculated as follows:

   .. table:: **Table 1** Number of NameNode file objects

      +--------------------------------+---------------------------------------------------------+
      | Size of a File                 | Number of File Objects                                  |
      +================================+=========================================================+
      | < 128 MB                       | 1 (File) + 1 (Block) = 2                                |
      +--------------------------------+---------------------------------------------------------+
      | > 128 MB (for example, 128 GB) | 1 (File) + 1,024 (128 GB/128 MB = 1,024 blocks) = 1,025 |
      +--------------------------------+---------------------------------------------------------+

   The maximum number of file objects supported by the active and standby NameNodes is 300,000,000 (equivalent to 150,000,000 small files). **dfs.namenode.max.objects** specifies the number of file objects that can be generated in the system. The default value is **0**, which indicates that the number of generated file objects is not limited.

-  DataNode capacity specifications

   In HDFS, blocks are stored on the DataNode as copies. The default number of copies is **3**, which can be set in the **dfs.replication** parameter.

   The number of blocks stored on all DataNode role instances in the cluster can be calculated based on the following formula: Number of HDFS blocks x 3 Average number of saved blocks = Number of HDFS blocks x 3/Number of DataNodes

   .. table:: **Table 2** DataNode specifications

      +----------------------------------------------------------------------------------------------------------------+----------------+
      | Item                                                                                                           | Specifications |
      +================================================================================================================+================+
      | Maximum number of block supported by a DataNode instance                                                       | 5,000,000      |
      +----------------------------------------------------------------------------------------------------------------+----------------+
      | Maximum number of block supported by a disk on a DataNode instance                                             | 500,000        |
      +----------------------------------------------------------------------------------------------------------------+----------------+
      | Minimum number of disks required when the number of block supported by a DataNode instance reaches the maximum | 10             |
      +----------------------------------------------------------------------------------------------------------------+----------------+

   .. table:: **Table 3** Number of DataNodes

      ===================== ================================
      Number of HDFS Blocks Minimum Number of DataNode Roles
      ===================== ================================
      10,000,000            10,000,000 \*3/5,000,000 = 6
      50,000,000            50,000,000 \*3/5,000,000 = 30
      100,000,000           100,000,000 \*3/5,000,000 = 60
      ===================== ================================

Setting Memory Parameters
-------------------------

-  Configuration rules of the NameNode JVM parameter

   Default value of the NameNode JVM parameter **GC_OPTS**:

   -Xms2G -Xmx4G -XX:NewSize=128M -XX:MaxNewSize=256M -XX:MetaspaceSize=128M -XX:MaxMetaspaceSize=128M -XX:+UseConcMarkSweepGC -XX:+CMSParallelRemarkEnabled -XX:CMSInitiatingOccupancyFraction=65 -XX:+PrintGCDetails -Dsun.rmi.dgc.client.gcInterval=0x7FFFFFFFFFFFFFE -Dsun.rmi.dgc.server.gcInterval=0x7FFFFFFFFFFFFFE -XX:-OmitStackTraceInFastThrow -XX:+PrintGCDateStamps -XX:+UseGCLogFileRotation -XX:NumberOfGCLogFiles=10 -XX:GCLogFileSize=1M -Djdk.tls.ephemeralDHKeySize=2048

   The number of NameNode files is proportional to the used memory size of the NameNode. When file objects change, you need to change **-Xms2G -Xmx4G -XX:NewSize=128M --XX:MaxNewSize=256M** in the default value. The following table lists the reference values.

   .. table:: **Table 4** NameNode JVM configuration

      +------------------------+------------------------------------------------------+
      | Number of File Objects | Reference Value                                      |
      +========================+======================================================+
      | 10,000,000             | -Xms6G -Xmx6G -XX:NewSize=512M -XX:MaxNewSize=512M   |
      +------------------------+------------------------------------------------------+
      | 20,000,000             | -Xms12G -Xmx12G -XX:NewSize=1G -XX:MaxNewSize=1G     |
      +------------------------+------------------------------------------------------+
      | 50,000,000             | -Xms32G -Xmx32G -XX:NewSize=3G -XX:MaxNewSize=3G     |
      +------------------------+------------------------------------------------------+
      | 100,000,000            | -Xms64G -Xmx64G -XX:NewSize=6G -XX:MaxNewSize=6G     |
      +------------------------+------------------------------------------------------+
      | 200,000,000            | -Xms96G -Xmx96G -XX:NewSize=9G -XX:MaxNewSize=9G     |
      +------------------------+------------------------------------------------------+
      | 300,000,000            | -Xms164G -Xmx164G -XX:NewSize=12G -XX:MaxNewSize=12G |
      +------------------------+------------------------------------------------------+

-  Configuration rules of the DataNode JVM parameter

   Default value of the DataNode JVM parameter **GC_OPTS**:

   -Xms2G -Xmx4G -XX:NewSize=128M -XX:MaxNewSize=256M -XX:MetaspaceSize=128M -XX:MaxMetaspaceSize=128M -XX:+UseConcMarkSweepGC -XX:+CMSParallelRemarkEnabled -XX:CMSInitiatingOccupancyFraction=65 -XX:+PrintGCDetails -Dsun.rmi.dgc.client.gcInterval=0x7FFFFFFFFFFFFFE -Dsun.rmi.dgc.server.gcInterval=0x7FFFFFFFFFFFFFE -XX:-OmitStackTraceInFastThrow -XX:+PrintGCDateStamps -XX:+UseGCLogFileRotation -XX:NumberOfGCLogFiles=10 -XX:GCLogFileSize=1M -Djdk.tls.ephemeralDHKeySize=2048

   The average number of blocks stored in each DataNode instance in the cluster is: Number of HDFS blocks x 3/Number of DataNodes. If the average number of blocks changes, you need to change **-Xms2G -Xmx4G -XX:NewSize=128M -XX:MaxNewSize=256M** in the default value. The following table lists the reference values.

   .. table:: **Table 5** DataNode JVM configuration

      +-------------------------------------------------+----------------------------------------------------+
      | Average Number of Blocks in a DataNode Instance | Reference Value                                    |
      +=================================================+====================================================+
      | 2,000,000                                       | -Xms6G -Xmx6G -XX:NewSize=512M -XX:MaxNewSize=512M |
      +-------------------------------------------------+----------------------------------------------------+
      | 5,000,000                                       | -Xms12G -Xmx12G -XX:NewSize=1G -XX:MaxNewSize=1G   |
      +-------------------------------------------------+----------------------------------------------------+

   **Xmx** specifies memory which corresponds to the threshold of the number of DataNode blocks, and each GB memory supports a maximum of 500,000 DataNode blocks. Set the memory as required.

Viewing the HDFS Capacity Status
--------------------------------

-  NameNode information

   Log in to FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS** > **NameNode(Active)**, and click **Overview** to view information like the number of file objects, files, directories, and blocks in HDFS in **Summary** area.

-  DataNode information

   Log in to FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS** > **NameNode(Active)**, and click **DataNodes** to view the number of blocks on all DataNodes that report alarms.

-  Alarm information

   Check whether the alarms whose IDs are 14007, 14008, and 14009 are generated and change the alarm thresholds as required.
