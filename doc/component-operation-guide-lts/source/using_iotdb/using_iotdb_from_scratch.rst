:original_name: mrs_01_24157.html

.. _mrs_01_24157:

Using IoTDB from Scratch
========================

IoTDB is a data management engine that integrates collection, storage, and analysis of time series data. It features lightweight, high performance, and ease of use. It perfectly interconnects with the Hadoop and Spark ecosystems and meets the requirements of high-speed write and complex analysis and query on massive time series data in industrial IoT applications.

Background
----------

Assume that a group has three production lines with five devices on each. Sensors collect indicators (such as temperature, speed, and running status) of these devices in real time, as shown in :ref:`Figure 1 <mrs_01_24157__fig129001748528>`. The service process of storing and managing data using IoTDB is as follows:

#. Create a storage group named **root.**\ *Group name* to represent the group.
#. Create time series to store the device indicators.
#. Simulate sensors and record indicators.
#. Run SQL statements to query indicators.
#. After the service is complete, delete the stored data.

.. _mrs_01_24157__fig129001748528:

.. figure:: /_static/images/en-us_image_0000001532951892.png
   :alt: **Figure 1** Data structure

   **Figure 1** Data structure

Procedure
---------

#. Log in to the client.

   a. Log in to the node where the client is installed as the client installation user and run the following command to switch to the client installation directory, for example, **/opt/client**.

      **cd /opt/client**

   b. Run the following command to configure environment variables:

      **source bigdata_env**

   c. .. _mrs_01_24157__li10203101511564:

      If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the current user. The current user must have the permission to create IoTDB tables. For details, see :ref:`IoTDB Permission Management <mrs_01_24140>`. If Kerberos authentication is disabled for the current cluster, skip this step.

      **kinit** *MRS cluster user*

      Example:

      **kinit iotdbuser**

#. Run the following command to switch to the directory where the script for running IoTDB client is stored:

   **cd /opt/client/IoTDB/iotdb/sbin**

#. Run the following command to log in to the client:

   **./start-cli.sh -h** *IP address of the IoTDBServer instance node* **-p** *IoTDBServer RPC port*

   The default IoTDBServer RPC port number is **22260**, which can be configured in the **rpc_port** parameter.

   After you run this command, specify the service username as required.

   -  To specify the service username, enter **yes** and enter the service username and password as prompted.

      |image1|

   -  If you will not specify the service username, enter **no**. In this case, you will perform subsequent operations as the user in :ref:`1.c <mrs_01_24157__li10203101511564>`.

      |image2|

   -  If you enter other information, you will log out.

      |image3|

#. Create a storage group named **root.company** based on :ref:`Figure 1 <mrs_01_24157__fig129001748528>`.

   **set storage group to root.company;**

#. Create corresponding time series for sensors of the devices on the production line.

   **create timeseries root.company.line1.device1.spin WITH DATATYPE=FLOAT, ENCODING=RLE;**

   **create timeseries root.company.line1.device1.status WITH DATATYPE=BOOLEAN, ENCODING=PLAIN;**

   **create timeseries root.company.line1.device2.temperature WITH DATATYPE=FLOAT, ENCODING=RLE;**

   **create timeseries root.company.line1.device2.power WITH DATATYPE=FLOAT, ENCODING=RLE;**

   **create timeseries root.company.line2.device1.temperature WITH DATATYPE=FLOAT, ENCODING=RLE;**

   **create timeseries root.company.line2.device1.speed WITH DATATYPE=FLOAT, ENCODING=RLE;**

   **create timeseries root.company.line2.device2.speed WITH DATATYPE=FLOAT, ENCODING=RLE;**

   **create timeseries root.company.line2.device2.status WITH DATATYPE=BOOLEAN, ENCODING=PLAIN;**

#. Adds data to time series.

   **insert into root.company.line1.device1(timestamp, spin) values (now(), 6684.0);**

   **insert into root.company.line1.device1(timestamp, status) values (now(), false);**

   **insert into root.company.line1.device2(timestamp, temperature) values (now(), 66.7);**

   **insert into root.company.line1.device2(timestamp, power) values (now(), 996.4);**

   **insert into root.company.line2.device1(timestamp, temperature) values (now(), 2684.0);**

   **insert into root.company.line2.device1(timestamp, speed) values (now(), 120.23);**

   **insert into root.company.line2.device2(timestamp, speed) values (now(), 130.56);**

   **insert into root.company.line2.device2(timestamp, status) values (now(), false);**

#. Query indicators of all devices on the production line 1.

   **select \* from root.company.line1.**;**

   .. code-block::

      +-----------------------------+-------------------------------+---------------------------------+--------------------------------------+--------------------------------+
      |                         Time|root.company.line1.device1.spin|root.company.line1.device1.status|root.company.line1.device2.temperature|root.company.line1.device2.power|
      +-----------------------------+-------------------------------+---------------------------------+--------------------------------------+--------------------------------+
      |2021-06-17T11:29:08.131+08:00|                         6684.0|                             null|                                  null|                            null|
      |2021-06-17T11:29:08.220+08:00|                           null|                            false|                                  null|                            null|
      |2021-06-17T11:29:08.249+08:00|                           null|                             null|                                  66.7|                            null|
      |2021-06-17T11:29:08.282+08:00|                           null|                             null|                                  null|                           996.4|
      +-----------------------------+-------------------------------+---------------------------------+--------------------------------------+--------------------------------+

#. Delete all device indicators on the production line 2.

   **delete timeseries root.company.line2.*;**

   Query the indicator data on production line 2. The result shows no indicator data exists.

   **select \* from root.company.line2.**;**

   .. code-block::

      +----+
      |Time|
      +----+
      +----+
      Empty set.

.. |image1| image:: /_static/images/en-us_image_0000001583391869.png
.. |image2| image:: /_static/images/en-us_image_0000001582952105.png
.. |image3| image:: /_static/images/en-us_image_0000001532632212.png
