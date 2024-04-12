:original_name: mrs_01_24510.html

.. _mrs_01_24510:

Importing IoTDB Data
====================

Scenario
--------

This section describes how to use **import-csv.sh** to import data in CSV format to IoTDB.

Prerequisites
-------------

-  The client has been installed. For details, see . For example, the installation directory is **/opt/client**. The client directory in the following operations is only an example. Change it based on the actual installation directory onsite.
-  Service component users have been created by the MRS cluster administrator by referring to . In security mode, machine-machine users need to download the keytab file. For details, see . A human-machine user must change the password upon the first login.
-  By default, SSL is enabled on the server. You have generated the **truststore.jks** certificate by following the instructions provided in :ref:`Using the IoTDB Client <mrs_01_24158>` and copied it to the **Client installation directory/IoTDB/iotdb/conf** directory.

Procedure
---------

#. .. _mrs_01_24510__li4604150164718:

   Prepare a CSV file named **example-filename.csv** on the local PC with the following content:

   .. code-block::

      Time,root.fit.d1.s1,root.fit.d1.s2,root.fit.d2.s1,root.fit.d2.s3,root.fit.p.s1
      1,100,hello,200,300,400
      2,500,world,600,700,800
      3,900,"hello, \"world\"",1000,1100,1200

   .. important::

      Before importing data, pay attention to the following:

      -  The data to be imported cannot contain spaces. Otherwise, importing that line of data fails and is skipped, but subsequent import operations are not affected.
      -  Data that contains commas (,) must be enclosed in single or double quotation marks. For example, **hello,world** is changed to **"hello,world"**.
      -  Quotation marks ("") in the data must be replaced with the escape character **\\"**. For example, **"world"** is changed to **\\"world\\"**.
      -  Single quotation marks (') in the data must be replaced with the escape character **\\'**. For example, **'world'** will be changed to **\\'world\\'**.
      -  If the data to be imported is time, the format is **yyyy-MM-dd'T'HH:mm:ss**, **yyy-MM-dd HH:mm:ss** or **yyyy-MM-dd'T'HH:mm:ss.SSSZ**, for example, **2022-02-28T11:07:00**, **2022-02-28T11:07:00**, or **2022-02-28T11:07:00.000Z**.

#. Use WinSCP to import the CSV file to the directory of the node where the client is installed, for example, **/opt/client/IoTDB/iotdb/sbin**.

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to switch to the client installation directory:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. .. _mrs_01_24510__li16611562035:

   (Optional) Perform this step to authenticate the current user if Kerberos authentication is enabled for the cluster. If Kerberos authentication is not enabled, skip this step.

   **kinit** *Component service user*

#. Run the following command to switch to the directory where the IoTDB client running script is stored:

   **cd /opt/client/IoTDB/iotdb/sbin**

#. .. _mrs_01_24510__li05599513462:

   Run the following command to log in to the client:

   **./start-cli.sh** **-h** *Service IP address of the IoTDBServer instance node* **-p** *IoTDBServer RPC port*

   .. note::

      -  You can log in to FusionInsight Manager and choose **Cluster** > **Services** > **IoTDB** > **Instance** to view the service IP address of the IoTDBServer instance node.
      -  The default RPC port number is **22260**. To obtain the port number, choose **Cluster** > **Services** > **IoTDB**, choose **Configurations** > **All Configurations**, and search for **rpc_port**.

   After you run this command, specify the service username as required.

   -  To specify the service username, enter **yes** and enter the service username and password as prompted.

      |image1|

   -  If you will not specify the service username, enter **no**. In this case, you will perform subsequent operations as the user in :ref:`6 <mrs_01_24510__li16611562035>`.

      |image2|

   -  If you enter other information, you will log out.

      |image3|

#. (Optional) Create metadata.

   IoTDB has the capability of type inference, so it is not necessary to create metadata before data import. However, it is recommended that you create metadata before using the CSV tool to import data, because this avoids unnecessary type conversion errors. The commands are as follows:

   .. code-block::

      SET STORAGE GROUP TO root.fit.d1;
      SET STORAGE GROUP TO root.fit.d2;
      SET STORAGE GROUP TO root.fit.p;
      CREATE TIMESERIES root.fit.d1.s1 WITH DATATYPE=INT32,ENCODING=RLE;
      CREATE TIMESERIES root.fit.d1.s2 WITH DATATYPE=TEXT,ENCODING=PLAIN;
      CREATE TIMESERIES root.fit.d2.s1 WITH DATATYPE=INT32,ENCODING=RLE;
      CREATE TIMESERIES root.fit.d2.s3 WITH DATATYPE=INT32,ENCODING=RLE;
      CREATE TIMESERIES root.fit.p.s1 WITH DATATYPE=INT32,ENCODING=RLE;

#. Run the following command to exit the client:

   **quit;**

#. Run the following command to switch to the directory where the **import-csv.sh** script is stored:

   **cd /opt/client/IoTDB/iotdb/tools**

#. Run the following command to run **import-csv.sh** and import the **example-filename.csv** file:

   **./import-csv.sh -h** *Service IP address of the IoTDBServer instance* **-p**\ *IoTDBServer RPC port* **-f** *example-filename.csv*

   Enter the service username and password in interactive mode as prompted. If information in the following figure is displayed, the CSV file is imported:

   |image4|

#. Verify data consistency.

   a. Run the following command to switch to the directory where the IoTDB client running script is stored:

      **cd /opt/client/IoTDB/iotdb/sbin**

   b. Log in to the IoTDB client by referring to :ref:`8 <mrs_01_24510__li05599513462>`. Run SQL statements to query data and compare the data with that in the :ref:`1 <mrs_01_24510__li4604150164718>` file.

   c. Check whether the imported data is consistent with the data in the :ref:`1 <mrs_01_24510__li4604150164718>`. If they are, the import is successful.

      Run the following command to check the imported data:

      **SELECT \* FROM root.fit.**;**

      |image5|

      .. note::

         -  To prevent security risks, you are advised to import CSV files in interactive mode.

         -  You can also import CSV files by running the **./import-csv.sh -h** *Service IP address of the IoTDBServer instance* **-p** *IoTDBServer RPC port* **-u** *Service username* **-pw** *Service user password*\ **-f** *example-filename.csv* command.

            If information in the following figure is displayed, the CSV file is imported.

            |image6|

         -  If nanosecond (ns) time precision is enabled for the IoTDB on the server, the **-tp ns** parameter needs to be added when the client imports data with the nanosecond timestamp. To check whether nanosecond time precision is enabled for a cluster, log in to FusionInsight Manager, choose **Cluster** > **Configurations** > **All Non-default Values**, and search for **timestamp_precision**.

.. |image1| image:: /_static/images/en-us_image_0000001532951928.png
.. |image2| image:: /_static/images/en-us_image_0000001583272201.png
.. |image3| image:: /_static/images/en-us_image_0000001582952133.png
.. |image4| image:: /_static/images/en-us_image_0000001532792008.png
.. |image5| image:: /_static/images/en-us_image_0000001532951944.png
.. |image6| image:: /_static/images/en-us_image_0000001583151917.png
