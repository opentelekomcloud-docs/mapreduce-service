:original_name: mrs_01_1610.html

.. _mrs_01_1610:

Performing an HBase DR Service Switchover
=========================================

Scenario
--------

The system administrator can configure HBase cluster DR to improve system availability. If the active cluster in the DR environment is faulty and the connection to the HBase upper-layer application is affected, you need to configure the standby cluster information for the HBase upper-layer application so that the application can run in the standby cluster.

Impact on the System
--------------------

After a service switchover, data written to the standby cluster is not synchronized to the active cluster by default. Add the active cluster is recovered, the data newly generated in the standby cluster needs to be synchronized to the active cluster by backup and recovery. If automatic data synchronization is required, you need to switch over the active and standby HBase DR clusters.

Procedure
---------

#. Log in to FusionInsight Manager of the standby cluster.

#. Download and install the HBase client.

#. On the HBase client of the standby cluster, run the following command as user **hbase** to enable the data writing status in the standby cluster.

   **kinit hbase**

   **hbase shell**

   **set_clusterState_active**

   The command is run successfully if the following information is displayed:

   .. code-block::

      hbase(main):001:0> set_clusterState_active
      => true

#. Check whether the original configuration files **hbase-site.xml**, **core-site.xml**, and **hdfs-site.xml** of the HBase upper-layer application are modified to adapt to the application running.

   -  If yes, update the related content to the new configuration file and replace the old configuration file.
   -  If no, use the new configuration file to replace the original configuration file of the HBase upper-layer application.

#. Configure the network connection between the host where the HBase upper-layer application is located and the standby cluster.

   .. note::

      If the host where the client is installed is not a node in the cluster, configure network connections for the client to prevent errors when you run commands on the client.

   a. Ensure that the host where the client is installed can communicate with the hosts listed in the **hosts** file in the directory where the client installation package is decompressed.
   b. If the host where the client is located is not a node in the cluster, you need to set the mapping between the host name and the IP address (service plan) in the /etc/hosts file on the host. The host names and IP addresses must be mapped one by one.

#. Set the time of the host where the HBase upper-layer application is located to be the same as that of the standby cluster. The time difference must be less than 5 minutes.

#. Check the authentication mode of the active cluster.

   -  If the security mode is used, go to :ref:`8 <mrs_01_1610__en-us_topic_0000001173470894_l5002f6a291d5455895e03939d56eae5c>`.
   -  If the normal mode is used, no further action is required.

#. .. _mrs_01_1610__en-us_topic_0000001173470894_l5002f6a291d5455895e03939d56eae5c:

   Obtain the **keytab** and **krb5.conf** configuration files of the HBase upper-layer application user.

   a. On FusionInsight Manager of the standby cluster, choose **System** > **Permission** > **User**.
   b. Locate the row that contains the target user, click **More** > **Download Authentication Credential** in the **Operation** column, and download the **keytab** file to the local PC.
   c. Decompress the package to obtain **user.keytab** and **krb5.conf**.

#. Use the **user.keytab** and **krb5.conf** files to replace the original files in the HBase upper-layer application.

#. Stop upper-layer applications.

#. Determine whether to switch over the active and standby HBase clusters. If the switchover is not performed, data will not be synchronized.

   -  If yes, switch over the active and standby HBase DR clusters. For details, see :ref:`Performing an HBase DR Active/Standby Cluster Switchover <mrs_01_1611>`. Then, go to :ref:`12 <mrs_01_1610__en-us_topic_0000001173470894_li11189185214483>`.
   -  If no, go to :ref:`12 <mrs_01_1610__en-us_topic_0000001173470894_li11189185214483>`.

#. .. _mrs_01_1610__en-us_topic_0000001173470894_li11189185214483:

   Start the upper-layer services.
