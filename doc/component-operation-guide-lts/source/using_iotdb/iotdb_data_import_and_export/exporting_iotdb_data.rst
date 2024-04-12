:original_name: mrs_01_24511.html

.. _mrs_01_24511:

Exporting IoTDB Data
====================

Scenario
--------

This section describes how to use **export-csv.sh** to export data from IoTDB to a CSV file.

.. important::

   Exporting data to CSV files may cause injection risks. Exercise caution when performing this operation.

Prerequisites
-------------

-  The client has been installed. For details, see . For example, the installation directory is **/opt/client**. The client directory in the following operations is only an example. Change it based on the actual installation directory onsite.
-  Service component users have been created by the MRS cluster administrator by referring to . In security mode, machine-machine users need to download the keytab file. For details, see . A human-machine user must change the password upon the first login.
-  By default, SSL is enabled on the server. You have generated the **truststore.jks** certificate by following the instructions provided in :ref:`Using the IoTDB Client <mrs_01_24158>` and copied it to the **Client installation directory/IoTDB/iotdb/conf** directory.

Procedure
---------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to switch to the client installation directory:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. (Optional) Perform this step to authenticate the current user if Kerberos authentication is enabled for the cluster. If Kerberos authentication is not enabled, skip this step.

   **kinit** *Component service user*

#. Run the following command to switch to the directory where the **export-csv.sh** script is stored:

   **cd /opt/client/IoTDB/iotdb/tools**

#. Before executing the export script, input some queries or specify some SQL files. If a SQL file contains multiple SQL statements, the SQL statements must be separated by newline characters. For example:

   .. code-block::

      select * from root.fit.d1
      select * from root.sg1.d1

#. .. _mrs_01_24511__li87641654151912:

   Execute **export-csv.sh** to export data.

   **./export-csv.sh -h** *Service IP address of the IoTDBServer instance* **-p** *IoTDBServer RPC port* **-td <directory> [-tf <time-format> -s <sqlfile>]**

   Example:

   .. code-block::

      ./export-csv.sh -h x.x.x.x -p 22260 -td ./
      # Or
      ./export-csv.sh -h x.x.x.x -p 22260 -td ./ -tf yyyy-MM-dd\ HH:mm:ss
      # Or
      ./export-csv.sh -h x.x.x.x -p 22260 -td ./ -s sql.txt
      # Or
      ./export-csv.sh -h x.x.x.x -p 22260 -td ./ -tf yyyy-MM-dd\ HH:mm:ss -s sql.txt

   .. note::

      -  You can log in to FusionInsight Manager, choose **Cluster** > **Services** > **IoTDB**, and click the **Instance** tab to view the service IP address of the IoTDBServer instance node.
      -  The default RPC port number is **22260**. To obtain the port number, choose **Cluster** > **Services** > **IoTDB**, click the **Configurations** tab and then **All Configurations**, and search for **rpc_port**.
      -  If the data exported contains a comma (,), it will be enclosed in double quotation marks (""). For example, **hello,world** is exported as **"hello,world"**.
      -  If the data exported contains double quotation marks (""), it will be enclosed in double quotation marks ("") and the original double quotation masks are replaced with **\\"**. For example, **"world"** is exported as **"\\"world\\""**

#. When you run the command in :ref:`7 <mrs_01_24511__li87641654151912>`, a message is displayed indicating that CSV injection may occur. Enter **yes** to continue the command. If you enter another value, the data export operation will be canceled.

   |image1|

   For example, after you enter **yes**, enter the service username and password as prompted. If information in the following figure is displayed, the data is exported:

   |image2|

   .. note::

      -  To prevent security risks, you are advised to export CSV files in interactive mode.

      -  You can also export CSV files by running the **./export-csv.sh -h** *Service IP address of the IoTDBServer instance* **-p** *IoTDBServer RPC port* **-u** *Service username* **-pw** *Service user password* **-td <directory> [-tf <time-format> -s <sqlfile>]** command.

         Example:

         .. code-block::

            ./export-csv.sh -h x.x.x.x -p 22260 -u test -pw Password -td ./
            # Or
            ./export-csv.sh -h x.x.x.x -p 22260 -u test -pw Password -td ./
            # Or
            ./export-csv.sh -h x.x.x.x -p 22260 -u test -pw Password -td ./ -s sql.txt
            # Or
            ./export-csv.sh -h x.x.x.x -p 22260 -u test -pw Password -td ./ -tf yyyy-MM-dd\ HH:mm:ss -s sql.txt

         If information in the following figure is displayed, the CSV file is exported:

         |image3|

.. |image1| image:: /_static/images/en-us_image_0000001583391913.png
.. |image2| image:: /_static/images/en-us_image_0000001582952137.png
.. |image3| image:: /_static/images/en-us_image_0000001532472784.png
