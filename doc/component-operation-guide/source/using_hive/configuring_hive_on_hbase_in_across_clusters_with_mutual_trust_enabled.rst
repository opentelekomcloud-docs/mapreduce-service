:original_name: mrs_01_24293.html

.. _mrs_01_24293:

Configuring Hive on HBase in Across Clusters with Mutual Trust Enabled
======================================================================

For mutually trusted Hive and HBase clusters with Kerberos authentication enabled, you can access the HBase cluster and synchronize its key configurations to HiveServer of the Hive cluster.

Prerequisites
-------------

The mutual trust relationship has been configured between the two security clusters with Kerberos authentication enabled.

Procedure for Configuring Hive on HBase Across Clusters
-------------------------------------------------------

#. Download the HBase configuration file and decompress it.

   a. Log in to FusionInsight Manager of the target HBase cluster and choose **Cluster** > **Services** > **HBase**.
   b. Choose **More** > **Download Client**.
   c. Download the HBase configuration file and choose **Configuration Files only** for **Select Client Type**.

#. Log in to FusionInsight Manager of the source Hive cluster.

#. Choose **Cluster** > **Services** > **Hive** and click the **Configurations** tab and then **All Configurations**. On the displayed page, add the following parameters to the **hive-site.xml** configuration file of the HiveServer role.

   Search for the following parameters in the **hbase-site.xml** configuration file of the downloaded HBase client and add them to HiveServer:

   -  hbase.security.authentication
   -  hbase.security.authorization
   -  hbase.zookeeper.property.clientPort
   -  hbase.zookeeper.quorum (The domain name needs to be converted into an IP address.)
   -  hbase.regionserver.kerberos.principal
   -  hbase.master.kerberos.principal

#. Save the configurations and restart Hive.
