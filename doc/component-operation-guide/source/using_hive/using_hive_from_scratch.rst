:original_name: mrs_01_0442.html

.. _mrs_01_0442:

Using Hive from Scratch
=======================

Hive is a data warehouse framework built on Hadoop. It maps structured data files to a database table and provides SQL-like functions to analyze and process data. It also allows you to quickly perform simple MapReduce statistics using SQL-like statements without the need of developing a specific MapReduce application. It is suitable for statistical analysis of data warehouses.

Background
----------

Suppose a user develops an application to manage users who use service A in an enterprise. The procedure of operating service A on the Hive client is as follows:

**Operations on common tables**:

-  Create the **user_info** table.
-  Add users' educational backgrounds and professional titles to the table.
-  Query user names and addresses by user ID.
-  Delete the user information table after service A ends.

.. _mrs_01_0442__en-us_topic_0037446806_table27353390:

.. table:: **Table 1** User information

   =========== ==== ====== === =======
   ID          Name Gender Age Address
   =========== ==== ====== === =======
   12005000201 A    Male   19  City A
   12005000202 B    Female 23  City B
   12005000203 C    Male   26  City C
   12005000204 D    Male   18  City D
   12005000205 E    Female 21  City E
   12005000206 F    Male   32  City F
   12005000207 G    Female 29  City G
   12005000208 H    Female 30  City H
   12005000209 I    Male   26  City I
   12005000210 J    Female 25  City J
   =========== ==== ====== === =======

Procedure
---------

#. .. _mrs_01_0442__l6b58a848ef0f4fe6a361d4ef0ac39fb8:

   Download the client configuration file.

   -  For versions earlier than MRS 3.x, perform the following operations:

      a. Log in to MRS Manager. For details, see :ref:`Accessing Manager <mrs_01_2123>`. Then, choose **Services**.

      b. Click **Download Client**.

         Set **Client Type** to **Only configuration files**, **Download to** to **Server**, and click **OK** to generate the client configuration file. The generated file is saved in the **/tmp/MRS-client** directory on the active management node by default.

   -  For MRS 3.\ *x* or later, perform the following operations:

      a. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`.

      b. Choose **Cluster** > *Name of the desired cluster* > **Dashboard** > **More** > **Download Client**.

      c. Download the cluster client.

         Set **Select Client Type** to **Configuration Files Only** , select a platform type, and click **OK** to generate the client configuration file which is then saved in the **/tmp/FusionInsight-Client/** directory on the active management node by default.

#. Log in to the active management node of Manager.

   -  For versions earlier than MRS 3.x, perform the following operations:

      a. On the MRS console, click **Clusters**, choose **Active Clusters**, and click a cluster name. On the **Nodes** tab, view the node names. The node whose name contains **master1** is the Master1 node, and the node whose name contains **master2** is the Master2 node.

         The active and standby management nodes of MRS Manager are installed on Master nodes by default. Because Master1 and Master2 are switched over in active and standby mode, Master1 is not always the active management node of MRS Manager. Run a command in Master1 to check whether Master1 is active management node of MRS Manager. For details about the command, see :ref:`2.d <mrs_01_0442__le8e7045cece741e8b6209b929a50ff22>`.

      b. Log in to the Master1 node using the password as user **root**. For details, see `Logging In to a Cluster <https://docs.otc.t-systems.com/en-us/usermanual/mrs/mrs_01_0083.html>`__.

      c. Run the following commands to switch to user **omm**:

         **sudo su - root**

         **su - omm**

      d. .. _mrs_01_0442__le8e7045cece741e8b6209b929a50ff22:

         Run the following command to check the active management node of MRS Manager:

         **sh ${BIGDATA_HOME}/om-0.0.1/sbin/status-oms.sh**

         In the command output, the node whose **HAActive** is **active** is the active management node, and the node whose **HAActive** is **standby** is the standby management node. In the following example, **mgtomsdat-sh-3-01-1** is the active management node, and **mgtomsdat-sh-3-01-2** is the standby management node.

         .. code-block::

            Ha mode
            double
            NodeName              HostName                      HAVersion          StartTime                HAActive             HAAllResOK           HARunPhase
            192-168-0-30          mgtomsdat-sh-3-01-1           V100R001C01        2014-11-18 23:43:02      active               normal               Actived
            192-168-0-24          mgtomsdat-sh-3-01-2           V100R001C01        2014-11-21 07:14:02      standby              normal               Deactived

      e. Log in to the active management node as user **root**, for example, node **192-168-0-30**.

   -  For MRS 3.\ *x* or later, perform the following operations:

      a. Log in to any node where Manager is deployed as user **root**.

      b. Run the following command to identify the active and standby nodes:

         **sh ${BIGDATA_HOME}/om-server/om/sbin/status-oms.sh**

         In the command output, the value of **HAActive** for the active management node is **active**, and that for the standby management node is **standby**. In the following example, **node-master1** is the active management node, and **node-master2** is the standby management node.

         .. code-block::

            HAMode
            double
            NodeName             HostName        HAVersion          StartTime                HAActive             HAAllResOK           HARunPhase
            192-168-0-30         node-master1    V100R001C01        2020-05-01 23:43:02      active               normal               Actived
            192-168-0-24         node-master2    V100R001C01        2020-05-01 07:14:02      standby              normal               Deactived

      c. Log in to the primary management node as user **root** and run the following command to switch to user **omm**:

         **sudo su - omm**

#. Run the following command to go to the client installation directory:

   **cd /opt/client**

   The cluster client has been installed in advance. The following client installation directory is used as an example. Change it based on the site requirements.

#. .. _mrs_01_0442__li15639738131312:

   Run the following command to update the client configuration for the active management node.

   **sh refreshConfig.sh /opt/client** *Full path of the client configuration file package*

   For example, run the following command:

   **sh refreshConfig.sh /opt/client** **/tmp/FusionInsight-Client/FusionInsight_Cluster_1_Services_Client.tar**

   If the following information is displayed, the configurations have been updated successfully.

   .. code-block::

       ReFresh components client config is complete.
       Succeed to refresh components client config.

   .. note::

      You can refer to Method 2 in `Updating a Client <https://docs.otc.t-systems.com/en-us/usermanual/mrs/mrs_01_0089.html>`__ to perform operations in steps :ref:`1 <mrs_01_0442__l6b58a848ef0f4fe6a361d4ef0ac39fb8>` to :ref:`4 <mrs_01_0442__li15639738131312>`.

#. Use the client on a Master node.

   a. On the active management node, for example, **192-168-0-30**, run the following command to switch to the client directory, for example, **/opt/client**.

      **cd /opt/client**

   b. Run the following command to configure environment variables:

      **source bigdata_env**

   c. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the current user:

      **kinit** *MRS cluster user*

      Example: user **kinit hiveuser**

      The current user must have the permission to create Hive tables. To create a role with the permission, refer to `Creating a Role <https://docs.otc.t-systems.com/en-us/usermanual/mrs/mrs_01_0343.html>`__. To bind the role to the current user, refer to `Creating a User <https://docs.otc.t-systems.com/en-us/usermanual/mrs/mrs_01_0345.html>`__.If Kerberos authentication is disabled, skip this step.

   d. Run the client command of the Hive component directly.

      **beeline**

#. Run the Hive client command to implement service A.

   **Operations on internal tables**:

   a. Create the **user_info** user information table according to :ref:`Table 1 <mrs_01_0442__en-us_topic_0037446806_table27353390>` and add data to it.

      **create table user_info(id string,name string,gender string,age int,addr string);**

      For MRS 1.\ *x*, MRS 3.\ *x*, or later, perform the following operations:

      **insert into table user_info(id,name,gender,age,addr) values("12005000201","A","Male",19,"City A");**

      For MRS 2.\ *x*, perform the following operations:

      **insert into table user_info values("12005000201","A","Male",19,"City A");**

   b. Add users' educational backgrounds and professional titles to the **user_info** table.

      For example, to add educational background and title information about user 12005000201, run the following command:

      **alter table user_info add columns(education string,technical string);**

   c. Query user names and addresses by user ID.

      For example, to query the name and address of user 12005000201, run the following command:

      **select name,addr from user_info where id='12005000201';**

   d. Delete the user information table.

      **drop table user_info;**

   **Operations on external partition tables**:

   Create an external partition table and import data.

   a. Create a path for storing external table data.

      **hdfs dfs -mkdir /hive/**

      **hdfs dfs -mkdir /hive/user_info**

   b. Create a table.

      **create external table user_info(id string,name string,gender string,age int,addr string) partitioned by(year string) row format delimited fields terminated by ' ' lines terminated by '\\n' stored as textfile location '/hive/user_info';**

      .. note::

         **fields terminated** indicates delimiters, for example, spaces.

         **lines terminated** indicates line breaks, for example, **\\n**.

         **/hive/user_info** indicates the path of the data file.

   c. Import data.

      #. Execute the insert statement to insert data.

         **insert into user_info partition(year="2018") values ("12005000201","A","Male",19,"City A");**

      #. Run the **load data** command to import file data.

         #. Create a file based on the data in :ref:`Table 1 <mrs_01_0442__en-us_topic_0037446806_table27353390>`. For example, the file name is **txt.log**. Fields are separated by space, and the line feed characters are used as the line breaks.

         #. Upload the file to HDFS.

            **hdfs dfs -put txt.log /tmp**

         #. Load data to the table.

            **load data inpath '/tmp/txt.log' into table user_info partition (year='2011');**

   d. Query the imported data.

      **select \* from user_info;**

   e. Delete the user information table.

      **drop table user_info;**

   f. Run the following command to exit:

      **!q**
