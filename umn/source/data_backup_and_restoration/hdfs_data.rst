:original_name: mrs_01_0445.html

.. _mrs_01_0445:

HDFS Data
=========

.. _mrs_01_0445__section2349182854814:

Establishing a Data Transmission Channel
----------------------------------------

-  If the source cluster and destination cluster are deployed in different VPCs in the same region, create a network connection between the two VPCs to establish a data transmission channel at the network layer. For details, see **Virtual Private Cloud > User Guide > VPC Peering Connection**.
-  If the source cluster and destination cluster are deployed in the same VPC but belong to different security groups, add security group rules to each security group on the VPC management console. In the security rules, **Protocol** is set to **ANY**, **Transfer Direction** is set to **Inbound**, and **Source** is set to **Security Group** (the security group of the peer cluster).

   -  To add an inbound rule to the security group of the source cluster, select the security group of the destination cluster in **Source**.
   -  To add an inbound rule to the security group of the destination cluster, select the security group of the source cluster in **Source**.

-  If the source and destination clusters are deployed in the same security group of the same VPC and Kerberos authentication is enabled for both clusters, configure mutual trust between the two clusters.

Backing Up HDFS Data
--------------------

Based on the regions of and network connectivity between the source cluster and destination cluster, data backup scenarios are classified as follows:

-  .. _mrs_01_0445__li529181519336:

   Same Region

   If the source cluster and destination cluster are in the same region, set up a network transmission channel. Use the DistCp tool to run the following command to copy the HDFS, HBase, Hive data files and Hive metadata backup files from the source cluster to the destination cluster.

   .. code-block::

      $HADOOP_HOME/bin/hadoop distcp <src> <dist> -p

   The following provides description about the parameters in the preceding command.

   -  **$HADOOP_HOME**: installation directory of the Hadoop client in the destination cluster
   -  **<src>**: HDFS directory of the source cluster
   -  **<dist>**: HDFS directory of the destination cluster

-  Different Regions

   If the source cluster and destination cluster are in different regions, use the DistCp tool to copy the source cluster data to OBS, and use the OBS cross-region replication function (For details, see **Object Storage Service > Console Operation Guide > Cross-Region Replication**) to copy the data to OBS in the region where the destination cluster resides. If DistCp is used, permission, owner, and group information cannot be set for files on OBS. In this case, you need to export and copy the HDFS metadata while exporting data to prevent the loss of HDFS file property information.

-  Migrating Data from an Offline Cluster to a Cloud

   You can use the following way to migrate data from an offline cluster to the cloud.

   -  Direct Connect

      Create a Direct Connect between the source cluster and destination cluster, enable the network between the offline cluster egress gateway and the online VPC, and execute the DistCp to copy the data by referring to the method provided in :ref:`Same Region <mrs_01_0445__li529181519336>`.

Backing Up HDFS Metadata
------------------------

HDFS metadata information to be exported includes file and folder permissions and owner/group information. You can run the following command on the HDFS client to export the metadata:

.. code-block::

   $HADOOP_HOME/bin/hdfs dfs -ls -R <migrating_path> > /tmp/hdfs_meta.txt

The following provides description about the parameters in the preceding command.

-  **$HADOOP_HOME**: installation directory of the Hadoop client in the source cluster
-  **<migrating_path>**: HDFS data directory to be migrated
-  **/tmp/hdfs_meta.txt**: local path for storing the exported metadata

.. note::

   If the source cluster can communicate with the destination cluster and you run the **hadoop distcp** command as a super administrator to copy data, you can add the **-p** parameter to enable DistCp to restore the metadata of the corresponding file in the destination cluster while copying data. In this case, skip this step.

HDFS File Property Restoration
------------------------------

Based on the exported permission information, run the HDFS commands in the background of the destination cluster to restore the file permission and owner and group information.

.. code-block::

   $HADOOP_HOME/bin/hdfs dfs -chmod <MODE> <path>
   $HADOOP_HOME/bin/hdfs dfs -chown <OWNER> <path>
