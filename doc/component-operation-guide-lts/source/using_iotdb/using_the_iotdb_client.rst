:original_name: mrs_01_24158.html

.. _mrs_01_24158:

Using the IoTDB Client
======================

Scenario
--------

This section describes how to use the IoTDB client in the O&M or service scenario.

Prerequisites
-------------

-  The client has been installed. For example, the installation directory is **/opt/client**. The client directory in the following operations is only an example. Change it based on the actual installation directory onsite.
-  Service component users have been created by the MRS cluster administrator. In security mode, machine-machine users need to download the keytab file. A human-machine user must change the password upon the first login.

Procedure
---------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to go to the client installation directory:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Run the following command to generate a client SSL certificate:

   **keytool -noprompt -import -alias myservercert -file ca.crt -keystore truststore.jks**

   After running this command, you are required to set a password.

#. Copy the generated **truststore.jks** file to the **Client installation directory/IoTDB/iotdb/conf** directory.

   **cp truststore.jks** *Client installation directory*\ **/IoTDB/iotdb/conf**

#. .. _mrs_01_24158__li15263191081118:

   Log in to the IoTDB client based on the cluster authentication mode.

   -  In security mode, run the following command to authenticate the user and log in to the IoTDB client:

      **kinit** *Component service user*

   -  Skip this step in normal mode.

#. Run the following command to switch to the directory where the IoTDB client running script is stored:

   **cd /opt/client/IoTDB/iotdb/sbin**

#. Run the following command to log in to the client:

   **./start-cli.sh** **-h** *IP address of the IoTDBServer instance node* **-p** *IoTDBServer RPC port*

   After you run this command, specify the service username as required.

   -  To specify the service username, enter **yes** and enter the service username and password as prompted.

      |image1|

   -  If you will not specify the service username, enter **no**. In this case, you will perform subsequent operations as the user in :ref:`6 <mrs_01_24158__li15263191081118>`.

      |image2|

   -  If you enter other information, you will log out.

      |image3|

   .. note::

      -  When you log in to the client, you can configure the **-maxRPC** parameter to control the number of lines of execution results to be printed at a time. The default value is **1000**. If the value of **-maxRPC** is less than or equal to 0, all results are printed at a time. This parameter is typically used to redirect SQL execution results.

      -  Meanwhile, you can optionally use the **-disableISO8601** parameter to control the display format of the time column in the query result. If this parameter is not specified, the time is displayed in YYYYMMDDHHMMSS format. If this parameter is specified, the timestamp is displayed.

      -  If the SSL configuration is disabled on the server, you need to disable it on the client as follows:

         **cd** *Client installation directory*\ **/IoTDB/iotdb/conf**

         **vi iotdb-client.env**

         Change the value of **iotdb_ssl_enable** to **false**, save the configuration, and exit.

         To check the SSL configuration of the server, log in to FusionInsight Manager, choose **Cluster** > **Services** > **IoTDB** > **Configurations**, and search for **SSL_ENABLE**. Value **true** indicates that SSL is enabled, and value **false** indicates that it is disabled.

#. After logging in to the client, you can run SQL statements.

.. |image1| image:: /_static/images/en-us_image_0000001532791960.png
.. |image2| image:: /_static/images/en-us_image_0000001583151877.png
.. |image3| image:: /_static/images/en-us_image_0000001583391873.png
