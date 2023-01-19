:original_name: mrs_01_2337.html

.. _mrs_01_2337:

Using DBeaver to Access HetuEngine
==================================

This section uses DBeaver 6.3.5 as an example to describe how to perform operations on HetuEngine.

Prerequisites
-------------

-  The DBeaver has been installed properly. Download the DBeaver software from https://dbeaver.io/files/6.3.5/.

   .. note::

      Currently, DBeaver 5.\ *x* and 6.\ *x* are supported.

-  A human-machine user has been created in the cluster. For details about how to create a user, see :ref:`Creating a HetuEngine User <mrs_01_1714>`.

Procedure
---------

Method 1: Using ZooKeeper to access HetuEngine

#. .. _mrs_01_2337__en-us_topic_0000001219029577_li1747527125:

   Download the HetuEngine client.

   a. Log in to FusionInsight Manager.

   b. Choose **Cluster** > **Services** > **HetuEngine** > **Dashboard**.

   c. In the upper right corner of the page, choose **More** > **Download Client** and download the **Complete Client** to the local PC as prompted.

   d. .. _mrs_01_2337__en-us_topic_0000001219029577_li1727232161619:

      Decompress the HetuEngine client package **FusionInsight_Cluster\_**\ *Cluster ID*\ **\_ HetuEngine\_Client.tar** to obtain the JDBC file and save it to a local directory, for example, **D:\\test**.

      .. note::

         Obtaining the JDBC file:

         Obtain the **hetu-jdbc-*.jar** file from the **FusionInsight_Cluster\_**\ *Cluster ID*\ **\_HetuEngine\_ClientConfig\\HetuEngine\\xxx\\** directory.

         Note: **xxx** can be **arm** or **x86**.

#. Download the Kerberos authentication file of the HetuEngine user.

   a. Log in to FusionInsight Manager.
   b. Choose **System** > **Permission** > **User**.
   c. Locate the row that contains the target HetuEngine user, click **More** in the **Operation** column, and select **Download Authentication Credential**.
   d. Decompress the downloaded package to obtain the **user.keytab** and **krb5.conf** files.

#. Log in to the node where the HSBroker role is deployed in the cluster as user **omm**, go to the **${BIGDATA_HOME}/FusionInsight_Hetu\_8.1.2.2/xxx\ \_HSBroker/etc/** directory, and download the **jaas-zk.conf** and **hetuserver.jks** files to the local PC.

   .. note::

      The version 8.1.2.2 is used as an example. Replace it with the actual version number.

   Modify the **jaas-zk.conf** file as follows. **keyTab** is the keytab file path of the user who accesses HetuEngine, and **principal** is *Username for accessing HetuEngine*\ **@Domain name in uppercase.COM**.

   .. code-block::

      Client {
      com.sun.security.auth.module.Krb5LoginModule required
      useKeyTab=true
      keyTab="D:\\tmp\\user.keytab"
      principal="admintest@HADOOP.COM"
      useTicketCache=false
      storeKey=true
      debug=true;
      };

#. Add the host mapping to the local **hosts** file. The content format is as follows:

   *Host IP address Host name*

   Example: 192.168.23.221 192-168-23-221

   .. note::

      The local **hosts** file in a Windows environment is stored in, for example, **C:\\Windows\\System32\\drivers\\etc**.

#. Configure the DBeaver startup file **dbeaver.ini**.

   a. Add the Java path to the file.

      .. code-block::

         -VM
         C:\Program Files\Java\jdk1.8.0_131\bin

   b. Set the ZooKeeper and Kerberos parameters by referring to the following parameters. Replace the file paths with the actual paths.

      .. code-block::

         -Dsun.security.krb5.debug=true
         -Djava.security.auth.login.config=D:\tmp\jaas-zk.conf
         -Dzookeeper.sasl.clientconfig=Client
         -Dzookeeper.auth.type=kerberos
         -Djava.security.krb5.conf=D:\tmp\krb5.conf

      .. note::

         -  The Greenwich Mean Time (GMT) is not supported. If the current time zone is GMT+, add **-Duser.timezone=UTC** to the **dbeaver.ini** file to change the time zone to UTC.
         -  If DBeaver is started, restart the DBeaver software for the new configuration items in the **dbeaver.ini** file to take effect.

#. Start the DBeaver, right-click **Database Navigator**, and click **Create New Connection**.

#. Search for **Presto** in the search box and double-click the Presto icon.

#. Click **Edit Driver Settings**.

#. Set **Class Name** to **io.prestosql.jdbc.PrestoDriver**.

#. Enter the URL of HetuEngine in the **URL Template** text box.

   URL format: jdbc:presto://*IP address of node 1 where the ZooKeeper service resides*:2181,\ *IP address of node 2 where the ZooKeeper service resides*:2181,\ *IP address of node 3 where the ZooKeeper service resides*:2181/hive/default?serviceDiscoveryMode=zooKeeper&zooKeeperNamespace=hsbroker&zooKeeperServerPrincipal=zookeeper/hadoop.hadoop.com

   Example: **jdbc:presto://192.168.8.37:**\ 2181\ **,192.168.8.38:**\ 2181\ **,192.168.8.39:**\ 2181\ **/hive/default?serviceDiscoveryMode=zooKeeper&zooKeeperNamespace=hsbroker&zooKeeperServerPrincipal=zookeeper/hadoop.hadoop.com**

#. Click **Add File** and select the obtained JDBC file obtained in :ref:`1.d <mrs_01_2337__en-us_topic_0000001219029577_li1727232161619>`.

#. Click **Connection properties**. On the **Connection properties** tab page, right-click and select **Add new property**. Set parameters by referring to :ref:`Table 1 <mrs_01_2337__en-us_topic_0000001219029577_table1173517153344>`.

   .. _mrs_01_2337__en-us_topic_0000001219029577_table1173517153344:

   .. table:: **Table 1** Property information

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Example Value                                                                                                                             |
      +===================================+===========================================================================================================================================+
      | KerberosPrincipal                 | zhangsan                                                                                                                                  |
      |                                   |                                                                                                                                           |
      |                                   | .. note::                                                                                                                                 |
      |                                   |                                                                                                                                           |
      |                                   |    Human-machine user created in the cluster. For details, see :ref:`Creating a HetuEngine User <mrs_01_1714>`.                           |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
      | KerberosKeytabPath                | D:\\\\user.keytab                                                                                                                         |
      |                                   |                                                                                                                                           |
      |                                   | .. note::                                                                                                                                 |
      |                                   |                                                                                                                                           |
      |                                   |    You need to configure this parameter when using the keytab mode for access.                                                            |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
      | KerberosRemoteServiceName         | HTTP                                                                                                                                      |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
      | SSL                               | true                                                                                                                                      |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
      | deploymentMode                    | on_yarn                                                                                                                                   |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
      | tenant                            | default                                                                                                                                   |
      |                                   |                                                                                                                                           |
      |                                   | .. note::                                                                                                                                 |
      |                                   |                                                                                                                                           |
      |                                   |    The tenant to which the user belongs needs to be configured in the cluster.                                                            |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
      | user                              | zhangsan                                                                                                                                  |
      |                                   |                                                                                                                                           |
      |                                   | .. note::                                                                                                                                 |
      |                                   |                                                                                                                                           |
      |                                   |    Human-machine user created in the cluster. For details, see :ref:`Creating a HetuEngine User <mrs_01_1714>`.                           |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
      | password                          | zhangsan@##65331853                                                                                                                       |
      |                                   |                                                                                                                                           |
      |                                   | .. note::                                                                                                                                 |
      |                                   |                                                                                                                                           |
      |                                   |    -  Password set when a human-machine user is created in the cluster. For details, see :ref:`Creating a HetuEngine User <mrs_01_1714>`. |
      |                                   |    -  You need to configure this parameter when using username and password for access.                                                   |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
      | KerberosConfigPath                | D:\\\\krb5.conf                                                                                                                           |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
      | SSLTrustStorePath                 | D:\\\\hetuserver.jks                                                                                                                      |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+

   :ref:`Figure 1 <mrs_01_2337__en-us_topic_0000001219029577_fig16912205184112>` shows an example of the parameter settings.

   .. _mrs_01_2337__en-us_topic_0000001219029577_fig16912205184112:

   .. figure:: /_static/images/en-us_image_0000001438431645.png
      :alt: **Figure 1** Example of parameter settings

      **Figure 1** Example of parameter settings

#. Click **OK**.

#. Click **Finish**. The HetuEngine is successfully connected.

   .. note::

      If a message is displayed indicating that you do not have the permission to view the table, configure the permission by referring to :ref:`Configuring Permissions for Tables, Columns, and Databases <mrs_01_2352>`.

Method 2: Using HSBroker to access HetuEngine

#. .. _mrs_01_2337__en-us_topic_0000001219029577_li29221671357:

   Obtain the JDBC JAR file by referring to :ref:`1 <mrs_01_2337__en-us_topic_0000001219029577_li1747527125>`.

#. Open DBeaver, choose **Database** > **New Database Connection**, search for PrestoSQL, and open it.

#. Click **Edit Driver Settings** and set parameters by referring to the following table.

   .. table:: **Table 2** Driver settings

      +-----------------------+--------------------------------+----------------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Value                          | Remarks                                                                                                                    |
      +=======================+================================+============================================================================================================================+
      | Class Name            | io.prestosql.jdbc.PrestoDriver | /                                                                                                                          |
      +-----------------------+--------------------------------+----------------------------------------------------------------------------------------------------------------------------+
      | URL Template          | URL of HetuEngine              | URL format:                                                                                                                |
      |                       |                                |                                                                                                                            |
      |                       |                                | jdbc:presto://<*HSBrokerIP1:port1*>,<*HSBrokerIP2:port2*>,<*HSBrokerIP3:port3*>/hive/default?serviceDiscoveryMode=hsbroker |
      +-----------------------+--------------------------------+----------------------------------------------------------------------------------------------------------------------------+

#. Click **Add File** and upload the JDBC driver package obtained in :ref:`1 <mrs_01_2337__en-us_topic_0000001219029577_li29221671357>`.

#. Click **Find Class**. The driver class is automatically obtained. Click **OK** to complete the driver setting, as shown in :ref:`Figure 2 <mrs_01_2337__en-us_topic_0000001219029577_fig7280201602711>`.

   .. _mrs_01_2337__en-us_topic_0000001219029577_fig7280201602711:

   .. figure:: /_static/images/en-us_image_0000001441091233.png
      :alt: **Figure 2** Driver settings

      **Figure 2** Driver settings

#. On the **Main** tab page for creating a connection, enter the user name and password, and click **Test Connection**. After the connection is successful, click **OK**, and then click **Finish**.


   .. figure:: /_static/images/en-us_image_0000001349259429.png
      :alt: **Figure 3** Creating a connection

      **Figure 3** Creating a connection

#. After the connection is successful, the page shown in :ref:`Figure 4 <mrs_01_2337__en-us_topic_0000001219029577_fig18372036443>` is displayed.

   .. _mrs_01_2337__en-us_topic_0000001219029577_fig18372036443:

   .. figure:: /_static/images/en-us_image_0000001441208981.png
      :alt: **Figure 4** Successful connection

      **Figure 4** Successful connection
