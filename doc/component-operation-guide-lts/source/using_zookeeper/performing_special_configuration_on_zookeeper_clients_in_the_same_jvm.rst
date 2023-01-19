:original_name: mrs_01_2102.html

.. _mrs_01_2102:

Performing Special Configuration on ZooKeeper Clients in the Same JVM
=====================================================================

Scenarios
---------

Currently, ZooKeeper client properties can be configured only through Java system properties. Therefore, all clients in the same JVM have the same configuration. In some cases, the ZooKeeper client needs to connect to different clusters and this requires different client configurations. For example, if users want to connect two different ZooKeeper clusters from the same JVM, one cluster has the security mode enabled and the other does not. The configuration of each client varies. Different configuration methods are required for different clients.

This solution allows each ZooKeeper client to use different configurations. As shown in :ref:`Figure 1 <mrs_01_2102__en-us_topic_0000001219029643_fa44c1a23b67d492da21c48348fcd9fc5>`, each client uses different configurations, which are initialized in the property file.

.. _mrs_01_2102__en-us_topic_0000001219029643_fa44c1a23b67d492da21c48348fcd9fc5:

.. figure:: /_static/images/en-us_image_0000001349139437.png
   :alt: **Figure 1** Performing special configuration on ZooKeeper clients in the same JVM

   **Figure 1** Performing special configuration on ZooKeeper clients in the same JVM

Configuration Description
-------------------------

#. Create the ZKClientConfig instance and transfer the ZKClientConfig instance to ZooKeeper when creating the ZooKeeper instance.

   The methods for creating the ZKClientConfig instance are as follows:

   -  Method 1:

      .. code-block::

         ZKClientConfig clientConfig = new ZKClientConfig();

      ZKClientConfig will have all properties of the ZooKeeper client configured in Java.

   -  Method 2:

      .. code-block::

         ZKClientConfig clientConfig = new ZKClientConfig();
         clientConfig.addConfiguration("/somepath/zoo-client.cfg");

      ZKClientConfig is initialized in the **zoo-client.cfg** file. The properties of the **zoo-client.cfg** file will overwrite the same Java system properties.

   -  Method 3:

      .. code-block::

         ZKClientConfig clientConfig = new ZKClientConfig();
         clientConfig.setProperty(ZKClientConfig.SECURE_CLIENT, "true");

      After initialization, the clientConfig has the Java system properties. In addition, the additional property **ZKClientConfig.SECURE_CLIENT** is added through the code **clientConfig.setProperty(ZKClientConfig.SECURE_CLIENT, "true**").

#. After the configuration is complete, use any of the following ZooKeeper APIs to create a client.

   .. code-block::

      org.apache.zookeeper.ZooKeeper.ZooKeeper(String, int, Watcher, ZKClientConfig)
      org.apache.zookeeper.ZooKeeper.ZooKeeper(String, int, Watcher, boolean, ZKClientConfig)

Example Code
------------

Use the following code to connect Client1 and Client2 from the same JVM to a cluster with security mode enabled and a cluster in general mode, respectively.

-  Connect to a cluster with security mode enabled:

   .. code-block::

      String secureClientConfigPath = "/somepath/zoo-secure-client.cfg";
      ZKClientConfig secureClientConfig = new ZKClientConfig(secureClientConfigPath);
      ZooKeeper secureZooKeeperClient = new ZooKeeper(connectString, sessionTimeout, watcher, secureClientConfig);

-  Connect to a cluster in common mode:

   .. code-block::

      String nonSecureClientConfigPath = "/somepath/zoo-non-secure-client.cfg";

      File nonSecureConfigFile = new File(nonSecureClientConfigPath);
      ZKClientConfig nonSecureClientConfig = new ZKClientConfig(nonSecureConfigFile);
      ZooKeeper nonSecureZooKeeperClient = new ZooKeeper(connectString, sessionTimeout, watcher, nonSecureClientConfig);

Constraints
-----------

When Kerberos realms are different, we can map to KDC by the realm. Therefore, authentication can be performed based on the KDC of the realm of each client.

For example, two KDCs run on 192.168.1.2 and 192.168.1.3. The two KDCs correspond to the realms of HADOOP.COM and EXAMPLE.COM, respectively.

You can map KDC in the **krb5.conf** file based on the realm as follows:

.. code-block::

   [realms]
   HADOOP.COM = {
   kdc=192.168.1.2
   admin_server=192.168.1.2
   other attributes ...
   }

.. code-block::

   EXAMPLE.COM = {
   kdc=192.168.1.3
   admin_server=192.168.1.3
   other attributes ...
   }

However, when different KDCs have the same realm, the realm cannot map to the corresponding KDC. This is the configuration constraint of multiple ZooKeeper clients in the same JVM. Therefore, multiple ZooKeeper clients in the same JVM, cannot use multiple KDCs with the same realm.
