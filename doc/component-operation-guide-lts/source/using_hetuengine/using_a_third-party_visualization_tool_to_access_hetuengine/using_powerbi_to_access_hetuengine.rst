:original_name: mrs_01_24012.html

.. _mrs_01_24012:

Using PowerBI to Access HetuEngine
==================================

Prerequisites
-------------

-  PowerBI has been installed.
-  The JDBC JAR file has been obtained. For details, see :ref:`1 <mrs_01_2337__en-us_topic_0000001219029577_li1747527125>`.
-  A human-machine user has been created in the cluster. For details about how to create a user, see :ref:`Creating a HetuEngine User <mrs_01_1714>`.

Procedure
---------

#. Use the default configuration to install **hetu-odbc-win64.msi**. Download link: `https://openlookeng.io/download.html <https://openlookeng.io/en/download/>`__.


   .. figure:: /_static/images/en-us_image_0000001349259001.png
      :alt: **Figure 1** Downloading the driver

      **Figure 1** Downloading the driver

#. Configure data source driver.

   a. Run the following commands in the local command prompt to stop the ODBC service that is automatically started.

      **cd C:\\Program Files\\openLooKeng\\openLooKeng ODBC Driver 64-bit\\odbc_gateway\\mycat\\bin**

      **mycat.bat stop**

      |image1|

   b. Replace the JDBC driver.

      Copy the JDBC JAR file obtained in :ref:`1 <mrs_01_2337__en-us_topic_0000001219029577_li1747527125>` to the **C:\\Program Files\\openLooKeng\\openLooKeng ODBC Driver 64-bit\\odbc_gateway\\mycat\\lib** directory and delete the original **hetu-jdbc-1.0.1.jar** file from the directory.

   c. Edit the protocol prefix of the ODBC **server.xml** file.

      Change the property value of **server.xml** in the **C:\\Program Files\\openLooKeng\\openLooKeng ODBC Driver 64-bit\\odbc_gateway\\mycat\\conf** directory from **<property name="jdbcUrlPrefix">jdbc:lk://</property>** to

      **<property name="jdbcUrlPrefix">jdbc:presto://</property>**.

   d. .. _mrs_01_24012__en-us_topic_0000001173470764_li13423101229:

      Configure the connection mode of using the user name and password.

      Create a **jdbc_param.properties** file in a user-defined path, for example, **C:\\hetu**, and add the following content to the file:

      .. code-block::

         user=admintest
         password=admintest@##65331853

      .. note::

         **user**: indicates the username of the created human-machine user, for example, **admintest**.

         **password**: indicates the password of the created human-machine user, for example, **admintest@##65331853**.

   e. Run the following commands to restart the ODBC service:

      **cd C:\\Program Files\\openLooKeng\\openLooKeng ODBC Driver 64-bit\\odbc_gateway\\mycat\\bin**

      **mycat.bat restart**

      .. note::

         The ODBC service must be stopped each time the configuration is modified. After the modification is complete, restart the ODBC service.

#. On the Windows **Control Panel**, enter **odbc** to search for the ODBC management program.

   |image2|

#. Choose **Add** > **openLookeng ODBC 1.1 Driver** > **Finish**.

   |image3|

#. Enter the name and description as shown in the following figure and click **Next**.

   |image4|

#. Configure parameters by referring to the following figure. Obtain **<HSBrokerIP1:port1>,<HSBrokerIP2:port2>,<HSBrokerIP3:port3>/hive/default?serviceDiscoveryMode=hsbroker** for **Connect URL** by referring to :ref:`2 <mrs_01_24010__en-us_topic_0000001173789310_li6197135010379>`. Select the **jdbc_param.properties** file prepared in :ref:`2.d <mrs_01_24012__en-us_topic_0000001173470764_li13423101229>` for **Connect Config**. Set **User name** to the user name that is used to download the credential.

   |image5|

#. Click **Test DSN** to test the connection. If the connection is successful and both **Catalog** and **Schema** contain content, the connection is successful. Click **Next**.

   |image6|

   |image7|

#. Click **Finish**.

   |image8|

#. To use PowerBI for interconnection, choose **Get data** > **All** > **ODBC** > **Connect**.

   |image9|

#. Select the data source to be added and click **OK**.


   .. figure:: /_static/images/en-us_image_0000001349259005.png
      :alt: **Figure 2** Adding a data source

      **Figure 2** Adding a data source

#. (Optional) Enter **User name** and **Password** of the user who downloads the credential, and click **Connect**.


   .. figure:: /_static/images/en-us_image_0000001296219336.png
      :alt: **Figure 3** Entering the database username and password

      **Figure 3** Entering the database username and password

#. After the connection is successful, all table information is displayed, as shown in :ref:`Figure 4 <mrs_01_24012__en-us_topic_0000001173470764_fig5250802327>`.

   .. _mrs_01_24012__en-us_topic_0000001173470764_fig5250802327:

   .. figure:: /_static/images/en-us_image_0000001349059549.png
      :alt: **Figure 4** Successful connection

      **Figure 4** Successful connection

.. |image1| image:: /_static/images/en-us_image_0000001295899864.png
.. |image2| image:: /_static/images/en-us_image_0000001348739725.png
.. |image3| image:: /_static/images/en-us_image_0000001349139417.png
.. |image4| image:: /_static/images/en-us_image_0000001296059704.png
.. |image5| image:: /_static/images/en-us_image_0000001295739900.png
.. |image6| image:: /_static/images/en-us_image_0000001296219332.png
.. |image7| image:: /_static/images/en-us_image_0000001295899860.png
.. |image8| image:: /_static/images/en-us_image_0000001349139413.png
.. |image9| image:: /_static/images/en-us_image_0000001295739896.png
