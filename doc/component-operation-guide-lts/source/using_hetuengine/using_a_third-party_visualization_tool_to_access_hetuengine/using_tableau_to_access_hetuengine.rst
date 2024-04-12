:original_name: mrs_01_24010.html

.. _mrs_01_24010:

Using Tableau to Access HetuEngine
==================================

Prerequisites
-------------

-  Tableau has been installed.
-  The JDBC JAR file has been obtained. For details, see :ref:`1 <mrs_01_2337__li599475416716>`.
-  A human-machine user has been created in the cluster. For details about how to create a user, see :ref:`Creating a HetuEngine User <mrs_01_1714>`.

Procedure
---------

#. Place the obtained JAR file to the Tableau installation directory, for example, **C:\\Program Files\\Tableau\\Drivers**.

#. .. _mrs_01_24010__en-us_topic_0000001173789310_li6197135010379:

   Open Tableau, select **Other databases (JDBC)**, enter the URL and the username and password of the created human-machine user, and click **Sign In**.

   |image1|

   URL format:

   jdbc:presto://<*HSBrokerIP1:port1*>,<*HSBrokerIP2:port2*>,<*HSBrokerIP3:port3*>/hive/default?serviceDiscoveryMode=hsbroker

   Example:

   jdbc:presto://192.168.8.37:29860,192.168.8.38:29860,192.168.8.39:29860/hive/default?serviceDiscoveryMode=hsbroker

   Obtain the HSBroker node and port number:

   a. Log in to FusionInsight Manager.
   b. Choose **Cluster** > **Services** > **HetuEngine** > **Role** > **HSBroker** to obtain the service IP addresses of all HSBroker instances.
   c. Choose **Cluster** > **Services** > **HetuEngine** > **Configurations** > **All Configurations** and search for **server.port** on the right to obtain the port number of HSBroker.

      .. note::

         -  You can select one or more normal brokers for the HSBroker node and port number.
         -  If the connection fails, disable the proxy and try again.

#. After the login is successful, drag the data table to be operated to the operation window on the right and refresh data.

.. |image1| image:: /_static/images/en-us_image_0000001348740145.png
