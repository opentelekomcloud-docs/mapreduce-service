:original_name: mrs_01_2337.html

.. _mrs_01_2337:

Using DBeaver to Access HetuEngine
==================================

Use DBeaver 7.2.0 as an example to describe how to access HetuEngine.

.. _mrs_01_2337__section10331142641215:

Prerequisites
-------------

-  The DBeaver has been installed properly. Download the DBeaver software from https://dbeaver.io/files/7.2.0/.
-  A human-machine user, for example, **hetu_user**, has been created in the cluster. For details, see :ref:`Creating a HetuEngine User <mrs_01_1714>`. For clusters with Ranger authentication enabled, the Ranger permission must be added to user **hetu_user** based on service requirements. For details, see :ref:`Adding a Ranger Access Permission Policy for HetuEngine <mrs_01_1862>`.
-  A compute instance has been created and is running properly. For details, see :ref:`Creating HetuEngine Compute Instances <mrs_01_1731>`.

Procedure
---------

#. .. _mrs_01_2337__li599475416716:

   Download the HetuEngine client to obtain the JDBC JAR package.

   a. Log in to FusionInsight Manager.
   b. Choose **Cluster** > **Services** > **HetuEngine** > **Dashboard**.
   c. In the upper right corner of the page, choose **More** > **Download Client** and download the **Complete Client** to the local PC as prompted.
   d. Decompress the HetuEngine client package **FusionInsight_Cluster\_**\ *Cluster ID*\ **\_ HetuEngine\_Client.tar** to obtain the JDBC file and save it to a local directory, for example, **D:\\test**.

      .. note::

         Obtaining the JDBC file:

         Decompress the package in the **FusionInsight_Cluster\_**\ *Cluster ID*\ **\_HetuEngine\_ClientConfig\\HetuEngine\\xxx\\** directory to obtain the **hetu-jdbc-*.jar** file.

         Note: **xxx** can be **arm** or **x86**.

#. Add the host mapping to the local **hosts** file.

   Add the mapping of the host where the instance is located in the HSFabric or HSBroker mode. The format is *Host IP address* *Host name*.

   Example: **192.168.42.90 server-2110081635-0001**

   .. note::

      The local **hosts** file in a Windows environment is stored in, for example, **C:\\Windows\\System32\\drivers\\etc**.

#. Open DBeaver, choose **Database** > **New Database Connection**, search for **PrestoSQL** in **ALL**, and open PrestoSQL.

#. Click **Edit Driver Settings** and set parameters by referring to the following table.

   .. table:: **Table 1** Driver settings

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Value                                                                                                                         |
      +===================================+===============================================================================================================================+
      | Class Name                        | io.prestosql.jdbc.PrestoDriver                                                                                                |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
      | URL Template                      | -  Accessing HetuEngine using HSFabric                                                                                        |
      |                                   |                                                                                                                               |
      |                                   |    jdbc:presto://<*HSFabricIP1:port1*>,<*HSFabricIP2:port2*>,<*HSFabricIP3:port3*>/hive/default?serviceDiscoveryMode=hsfabric |
      |                                   |                                                                                                                               |
      |                                   |    Example:                                                                                                                   |
      |                                   |                                                                                                                               |
      |                                   |    jdbc:presto://192.168.42.90:29902,192.168.42.91:29902,192.168.42.92:29902/hive/default?serviceDiscoveryMode=hsfabric       |
      |                                   |                                                                                                                               |
      |                                   | -  Accessing HetuEngine using HSBroker                                                                                        |
      |                                   |                                                                                                                               |
      |                                   |    jdbc:presto://<*HSBrokerIP1:port1*>,<*HSBrokerIP2:port2*>,<*HSBrokerIP3:port3*>/hive/default?serviceDiscoveryMode=hsbroker |
      |                                   |                                                                                                                               |
      |                                   |    Example:                                                                                                                   |
      |                                   |                                                                                                                               |
      |                                   |    jdbc:presto://192.168.42.90:29860,192.168.42.91:29860,192.168.42.92:29860/hive/default?serviceDiscoveryMode=hsbroker       |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      -  To obtain the IP addresses and port numbers of the HSFabric and HSBroker nodes, perform the following operations:

         a. Log in to FusionInsight Manager.

         b. Choose **Cluster** > **Services** > **HetuEngine**. Click the **Instance** tab to obtain the service IP addresses of all HSFabric or HSBroker instances. You can select one or more normal instances for connection.

         c. To obtain the port numbers, choose **Cluster** > **Services** > **HetuEngine**. Click **Configurations** then **All Configurations**.

            Search for **gateway.port** to obtain the HSFabric port number. The default port number is **29902** in security mode and **29903** in normal mode.

            Search for **server.port** to obtain the HSBroker port number. The default port number is **29860** in security mode and **29861** in normal mode.

      -  If the connection fails, disable the proxy and try again.

#. Click **Add File** and upload the JDBC driver package obtained in :ref:`1 <mrs_01_2337__li599475416716>`.

#. Click **Find Class**. The driver class is automatically obtained. Click **OK** to complete the driver setting. If **io.prestosql:presto-jdbc:RELEASE** exists in **Libraries**, delete it before clicking **Find Class**.


   .. figure:: /_static/images/en-us_image_0000001584317997.png
      :alt: **Figure 1** Configuring the driver in security mode

      **Figure 1** Configuring the driver in security mode

#. Configure the connection.

   -  Security mode (clusters with Kerberos authentication enabled):

      On the **Main** tab page for creating a connection, enter the user name and password created in :ref:`Prerequisites <mrs_01_2337__section10331142641215>`, and click **Test Connection**. After the connection is successful, click **OK** then **Finish**. You can click **Connection details (name, type, ... )** to change the connection name.


      .. figure:: /_static/images/en-us_image_0000001533678044.png
         :alt: **Figure 2** Configuring parameters on the Main tab in security mode

         **Figure 2** Configuring parameters on the Main tab in security mode

   -  Normal mode (clusters with Kerberos authentication disabled):

      On the **Main** tab page for creating a connection, set JDBC URL and leave Password blank.

      On the page for creating a connection, configure the parameters on the **Driver properties** tab. Set **user** to the user created in :ref:`Prerequisites <mrs_01_2337__section10331142641215>`. Click **Test Connection**. After the connection is successful, click **OK** then **Finish**. You can click **Connection details (name, type, ... )** to change the connection name.


      .. figure:: /_static/images/en-us_image_0000001533198872.png
         :alt: **Figure 3** Configuring parameters on the Driver properties tab in normal mode

         **Figure 3** Configuring parameters on the Driver properties tab in normal mode

#. After the connection is successful, the page shown in :ref:`Figure 4 <mrs_01_2337__fig296125555813>` is displayed.

   .. _mrs_01_2337__fig296125555813:

   .. figure:: /_static/images/en-us_image_0000001533358396.png
      :alt: **Figure 4** Successful connection

      **Figure 4** Successful connection
