:original_name: mrs_01_0368.html

.. _mrs_01_0368:

Using HBase from Scratch
========================

HBase is a column-based distributed storage system that features high reliability, performance, and scalability. This section describes how to use HBase from scratch, including how to update the client on the Master node in the cluster, create a table using the client, insert data in the table, modify the table, read data from the table, delete table data, and delete the table.

Background
----------

Suppose a user develops an application to manage users who use service A in an enterprise. The procedure of operating service A on the HBase client is as follows:

-  Create the **user_info** table.
-  Add users' educational backgrounds and titles to the table.
-  Query user names and addresses by user ID.
-  Query information by user name.
-  Deregister users and delete user data from the user information table.
-  Delete the user information table after service A ends.

.. _mrs_01_0368__en-us_topic_0229422393_en-us_topic_0173178212_en-us_topic_0037446806_table27353390:

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
   12005000210 J    Male   25  City J
   =========== ==== ====== === =======

Prerequisites
-------------

The client has been installed. For example, the client is installed in the **/opt/client** directory. The client directory in the following operations is only an example. Change it to the actual installation directory. Before using the client, download and update the client configuration file, and ensure that the active management node of Manager is available.

Procedure
---------

For versions earlier than MRS 3.x, perform the following operations:

#. Download the client configuration file.

   a. Log in to MRS Manager. For details, see :ref:`Accessing Manager <mrs_01_2123>`. Then, choose **Services**.

   b. Click **Download Client**.

      Set **Client Type** to **Only configuration files**, **Download To** to **Server**, and click **OK** to generate the client configuration file. The generated file is saved in the **/tmp/MRS-client** directory on the active management node by default. You can customize the file path.

#. Log in to the active management node of MRS Manager.

   a. On the **Node** tab page, view the **Name** parameter. The node that contains **master1** in its name is the Master1 node. The node that contains **master2** in its name is the Master2 node.

      The active and standby management nodes of MRS Manager are installed on Master nodes by default. Because Master1 and Master2 are switched over in active and standby mode, Master1 is not always the active management node of MRS Manager. Run a command in Master1 to check whether Master1 is active management node of MRS Manager. For details about the command, see :ref:`2.d <mrs_01_0368__en-us_topic_0229422393_en-us_topic_0173178212_le8e7045cece741e8b6209b929a50ff22>`.

   b. Log in to the Master1 node using the password as user **root**. For details, see `Logging In to an ECS <https://docs.otc.t-systems.com/usermanual/mrs/mrs_01_0083.html>`__.

   c. Run the following commands to switch to user **omm**:

      **sudo su - root**

      **su - omm**

   d. .. _mrs_01_0368__en-us_topic_0229422393_en-us_topic_0173178212_le8e7045cece741e8b6209b929a50ff22:

      Run the following command to check the active management node of MRS Manager:

      **sh ${BIGDATA_HOME}/om-0.0.1/sbin/status-oms.sh**

      In the command output, the node whose **HAActive** is **active** is the active management node, and the node whose **HAActive** is **standby** is the standby management node. In the following example, **mgtomsdat-sh-3-01-1** is the active management node, and **mgtomsdat-sh-3-01-2** is the standby management node.

      .. code-block::

         Ha mode
         double
         NodeName              HostName                      HAVersion          StartTime                HAActive             HAAllResOK           HARunPhase
         192-168-0-30          mgtomsdat-sh-3-01-1           V100R001C01        2019-11-18 23:43:02      active               normal               Actived
         192-168-0-24          mgtomsdat-sh-3-01-2           V100R001C01        2019-11-21 07:14:02      standby              normal               Deactived

   e. Log in to the active management node, for example, **192-168-0-30** of MRS Manager as user **root**, and run the following command to switch to user **omm**:

      **sudo su - omm**

#. Run the following command to switch to the client installation directory, for example, **/opt/client**:

   **cd /opt/client**

#. Run the following command to update the client configuration for the active management node.

   **sh refreshConfig.sh /opt/client** *Full path of the client configuration file package*

   For example, run the following command:

   **sh refreshConfig.sh /opt/client /tmp/MRS-client/MRS_Services_Client.tar**

   If the following information is displayed, the configurations have been updated successfully.

   .. code-block::

      ReFresh components client config is complete.
      Succeed to refresh components client config.

#. Use the client on a Master node.

   a. On the active management node where the client is updated, for example, node **192-168-0-30**, run the following command to go to the client directory:

      **cd /opt/client**

   b. Run the following command to configure environment variables:

      **source bigdata_env**

   c. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the current user. The current user must have the permission to create HBase tables. If Kerberos authentication is disabled for the current cluster, skip this step.

      **kinit** *MRS cluster user*

      For example, **kinit hbaseuser**.

   d. Run the following HBase client command:

      **hbase shell**

#. Run the following commands on the HBase client to implement service A.

   a. Create the **user_info** user information table according to :ref:`Table 1 <mrs_01_0368__en-us_topic_0229422393_en-us_topic_0173178212_en-us_topic_0037446806_table27353390>` and add data to it.

      **create** '*user_info*',{**NAME** => 'i'}

      For example, to add information about the user whose ID is 12005000201, run the following commands:

      **put** '*user_info*','*12005000201*','**i:name**','*A*'

      **put** '*user_info*','*12005000201*','**i:gender**','*Male*'

      **put** '*user_info*','*12005000201*','**i:age**','*19*'

      **put** '*user_info*','*12005000201*','**i:address**','*City A*'

   b. Add users' educational backgrounds and titles to the **user_info** table.

      For example, to add educational background and title information about user 12005000201, run the following commands:

      **put** '*user_info*','*12005000201*','**i:degree**','*master*'

      **put** '*user_info*','*12005000201*','**i:pose**','*manager*'

   c. Query user names and addresses by user ID.

      For example, to query the name and address of user 12005000201, run the following command:

      **scan**'*user_info*',{**STARTROW**\ =>'*12005000201*',\ **STOPROW**\ =>'*12005000201*',\ **COLUMNS**\ =>['**i:name**','**i:address**']}

   d. Query information by user name.

      For example, to query information about user A, run the following command:

      **scan**'*user_info*',{**FILTER**\ =>"SingleColumnValueFilter('i','name',=,'binary:*A*')"}

   e. Delete user data from the user information table.

      All user data needs to be deleted. For example, to delete data of user 12005000201, run the following command:

      **delete**'*user_info*','*12005000201*','i'

   f. Delete the user information table.

      **disable**'*user_info*'

      **drop** '*user_info*'

For MRS 3.x or later, perform the following operations:

#. Use the client on the active management node.

   a. Log in to the node where the client is installed as the client installation user and run the following command to switch to the client directory:

      **cd /opt/client**

   b. Run the following command to configure environment variables:

      **source bigdata_env**

   c. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the current user. The current user must have the permission to create HBase tables. If Kerberos authentication is disabled for the current cluster, skip this step.

      **kinit** *MRS cluster user*

      For example, **kinit hbaseuser**.

   d. Run the following HBase client command:

      **hbase shell**

#. Run the following commands on the HBase client to implement service A.

   a. Create the **user_info** user information table according to :ref:`Table 1 <mrs_01_0368__en-us_topic_0229422393_en-us_topic_0173178212_en-us_topic_0037446806_table27353390>` and add data to it.

      **create** '*user_info*',{**NAME** => 'i'}

      For example, to add information about the user whose ID is **12005000201**, run the following commands:

      **put** '*user_info*','*12005000201*','**i:name**','*A*'

      **put** '*user_info*','*12005000201*','**i:gender**','*Male*'

      **put** '*user_info*','*12005000201*','**i:age**','*19*'

      **put** '*user_info*','*12005000201*','**i:address**','*City A*'

   b. Add users' educational backgrounds and titles to the **user_info** table.

      For example, to add educational background and title information about user 12005000201, run the following commands:

      **put** '*user_info*','*12005000201*','**i:degree**','*master*'

      **put** '*user_info*','*12005000201*','**i:pose**','*manager*'

   c. Query user names and addresses by user ID.

      For example, to query the name and address of user 12005000201, run the following command:

      **scan**'*user_info*',{**STARTROW**\ =>'*12005000201*',\ **STOPROW**\ =>'*12005000201*',\ **COLUMNS**\ =>['**i:name**','**i:address**']}

   d. Query information by user name.

      For example, to query information about user A, run the following command:

      **scan**'*user_info*',{**FILTER**\ =>"SingleColumnValueFilter('i','name',=,'binary:*A*')"}

   e. Delete user data from the user information table.

      All user data needs to be deleted. For example, to delete data of user 12005000201, run the following command:

      **delete**'*user_info*','*12005000201*','i'

   f. Delete the user information table.

      **disable**'*user_info*'

      **drop** '*user_info*'
