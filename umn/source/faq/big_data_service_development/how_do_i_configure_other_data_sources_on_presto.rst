:original_name: mrs_03_1147.html

.. _mrs_03_1147:

How Do I Configure Other Data Sources on Presto?
================================================

In this section, MySQL is used as an example.

-  For MRS 1.\ *x* and 3.\ *x* clusters, do the following:

   #. Log in to the MRS management console.

   #. Click the name of the cluster to go to its details page.

   #. Click the **Components** tab and then **Presto** in the component list. On the page that is displayed, click the **Configurations** tab then the **All Configurations** sub-tab.

   #. On the Presto configuration page that is displayed, find **connector-customize**.

   #. Set **Name** and **Value** as follows:

      **Name**: **mysql.connector.name**

      **Value**: **mysql**

   #. Click the plus sign (+) to add three more fields and set **Name** and **Value** according to the table below. Then click **Save**.

      +---------------------------+-----------------------------------+--------------------------+
      | Name                      | Value                             | Description              |
      +===========================+===================================+==========================+
      | mysql.connection-url      | jdbc:mysql://xxx.xxx.xxx.xxx:3306 | Database connection pool |
      +---------------------------+-----------------------------------+--------------------------+
      | mysql.connection-user     | xxxx                              | Database username        |
      +---------------------------+-----------------------------------+--------------------------+
      | mysql.connection-password | xxxx                              | Database password        |
      +---------------------------+-----------------------------------+--------------------------+

   #. Restart the Presto service.

   #. Run the following command to connect to the Presto Server of the cluster:

      **presto_cli.sh --**\ *krb5-config*\ **-**\ *path* {krb5.conf path} --*krb5-principal* {User principal} --*krb5-keytab-path* {user.keytab path} --*user* {presto username}

   #. Log in to Presto and run the **show catalogs** command to check whether the data source list mysql of Presto can be queried.

      |image1|

      Run the **show schemas from mysql** command to query the MySQL database.

-  For MRS 2.\ *x* clusters, do the following:

   #. Create the **mysql.properties** configuration file containing the following content:

      connector.name=mysql

      connection-url=jdbc:mysql://mysqlIp:3306

      connection-user=Username

      connection-password=Password

      .. note::

         -  **mysqlIp** indicates the IP address of the MySQL instance, which must be able to communicate with the MRS network.
         -  The username and password are those used to log in to the MySQL database.

   #. Upload the configuration file to the **/opt/Bigdata/MRS_Current/1_14_Coordinator/etc/catalog/** directory on the master node (where the Coordinator instance resides) and the **/opt/Bigdata/MRS_Current/1_14_Worker/etc/catalog/** directory on the core node (depending on the actual directory in the cluster), and change the file owner group to **omm:wheel**.

   #. Restart the Presto service.

.. |image1| image:: /_static/images/en-us_image_0000001442654037.png
