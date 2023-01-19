:original_name: mrs_01_1711.html

.. _mrs_01_1711:

Using HetuEngine from Scratch
=============================

This section describes how to use HetuEngine to connect to the Hive data source and query database tables of the Hive data source of the cluster through HetuEngine.

Prerequisites
-------------

-  The HetuEngine and Hive services have been installed in the cluster and are running properly.
-  If Kerberos authentication has been enabled for the cluster, you need to create a HetuEngine user and grant related permissions to the user in advance. For details, see :ref:`Creating a HetuEngine User <mrs_01_1714>`. In addition, you need to configure the permissions to manage the databases, tables, and columns of the data source for the user using Ranger. For details, see :ref:`Adding a Ranger Access Permission Policy for HetuEngine <mrs_01_1862>`.
-  The cluster client has been installed, for example, in the **/opt/client** directory.

Procedure
---------

#. Create and start a HetuEngine compute instance.

   a. Log in to FusionInsight Manager as a HetuEngine administrator and choose **Cluster** > **Services** > **HetuEngine**. The **HetuEngine** service page is displayed.
   b. In the **Basic Information** area on the **Dashboard** tab page, click the link next to **HSConsole WebUI**. The HSConsole page is displayed.
   c. Click **Create Configuration** above the instance list. In the **Configure Instance** dialog box, configure parameters.

      #. In the **Basic Configuration** area, set **Resource Queue** to the tenant queue associated with the user.
      #. Configure parameters in the **Coordinator Container Resource Configuration**, **Worker Container Resource Configuration**, and **Advanced Configuration** areas based on the actual resource plan. For details about the parameter configuration, see :ref:`Creating HetuEngine Compute Instances <mrs_01_1731>` or retain the default values.
      #. Select **Start Now** and wait until the instance configuration is complete.

#. Log in to the node where the HetuEngine client is installed and run the following command to switch to the client installation directory:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If the cluster is in security mode, run the following command to perform security authentication. If the cluster is in normal mode, skip this step.

   **kinit** *HetuEngine operation user*

   Example:

   **kinit** **hetu_test**

   Enter the password as prompted and change the password upon your first login.

#. Run the following command to log in to the catalog of the data source:

   **hetu-cli --catalog** *Data source name*

   For example, run the following command:

   **hetu-cli --catalog** **hive**

   .. note::

      The default name of the Hive data source of the cluster is **hive**. If you need to connect to an external data source, configure the external data source on HSConsole by referring to :ref:`Configuring Data Sources <mrs_01_2314>`.

   .. code-block::

      java -Djava.security.auth.login.config=/opt/client/HetuEngine/hetuserver/conf/jaas.conf -Dzookeeper.sasl.clientconfig=Client -Dzookeeper.auth.type=kerberos -Djava.security.krb5.conf=/opt/client/KrbClient/kerberos/var/krb5kdc/krb5.conf -Djava.util.logging.config.file=/opt/client/HetuEngine/hetuserver/conf/hetuserver-client-logging.properties -jar /opt/client/HetuEngine/hetuserver/jars/hetu-cli-*-executable.jar --catalog hive --deployment-mode on_yarn --server https://10.112.17.189:24002,10.112.17.228:24002,10.112.17.150:24002?serviceDiscoveryMode=zooKeeper&zooKeeperNamespace=hsbroker --krb5-remote-service-name HTTP --krb5-config-path /opt/client/KrbClient/kerberos/var/krb5kdc/krb5.conf
      hetuengine>

#. Run the following command to view the database information:

   **show schemas;**

   .. code-block::

           Schema
      --------------------
       default
       information_schema
      (2 rows)
      Query 20200730_080535_00002_ct2eg, FINISHED, 3 nodes
      Splits: 36 total, 36 done (100.00%)
      0:02 [2 rows, 35B] [0 rows/s, 15B/s]
