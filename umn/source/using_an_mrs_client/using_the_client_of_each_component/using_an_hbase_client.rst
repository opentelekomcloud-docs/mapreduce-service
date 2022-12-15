:original_name: mrs_01_24187.html

.. _mrs_01_24187:

Using an HBase Client
=====================

Scenario
--------

This section describes how to use the HBase client in an O&M scenario or a service scenario.

Prerequisites
-------------

-  The client has been installed. For example, the installation directory is **/opt/hadoopclient**. The client directory in the following operations is only an example. Change it to the actual installation directory.

-  Service component users are created by the administrator as required.

   A machine-machine user needs to download the **keytab** file and a human-machine user needs to change the password upon the first login.

-  If a non-**root** user uses the HBase client, ensure that the owner of the HBase client directory is this user. Otherwise, run the following command to change the owner.

   **chown user:group -R** *Client installation directory*\ **/HBase**

Using the HBase Client (Versions Earlier Than MRS 3.x)
------------------------------------------------------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to go to the client directory:

   **cd** **/opt/hadoopclient**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the current user. The current user must have the permission to create HBase tables. For details about how to configure a role with corresponding permissions, see `Creating a Role <https://docs.otc.t-systems.com/usermanual/mrs/mrs_01_0343.html>`__ To bind a role to a user, see `Creating a User <https://docs.otc.t-systems.com/usermanual/mrs/mrs_01_0345.html>`__. If Kerberos authentication is disabled for the current cluster, skip this step.

   **kinit** *Component service user*

   For example, **kinit hbaseuser**.

#. Run the following HBase client command:

   **hbase shell**

Using the HBase Client (MRS 3.x or Later)
-----------------------------------------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to go to the client directory:

   **cd** **/opt/hadoopclient**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If you use the client to connect to a specific HBase instance in a scenario where multiple HBase instances are installed, run the following command to load the environment variables of the instance. Otherwise, skip this step. For example, to load the environment variables of the HBase2 instance, run the following command:

   **source HBase2/component_env**

#. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the current user. The current user must have the permission to create HBase tables. For details about how to configure a role with corresponding permissions, see `Creating a Role <https://docs.otc.t-systems.com/usermanual/mrs/mrs_01_0343.html>`__ To bind a role to a user, see `Creating a User <https://docs.otc.t-systems.com/usermanual/mrs/mrs_01_0345.html>`__. If Kerberos authentication is disabled for the current cluster, skip this step.

   **kinit** *Component service user*

   For example, **kinit hbaseuser**.

#. Run the following HBase client command:

   **hbase shell**

Common HBase client commands
----------------------------

The following table lists common HBase client commands. For more commands, see http://hbase.apache.org/2.2/book.html.

.. table:: **Table 1** HBase client commands

   +----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Command  | Description                                                                                                                                                                                                                     |
   +==========+=================================================================================================================================================================================================================================+
   | create   | Used to create a table, for example, **create 'test', 'f1', 'f2', 'f3'**.                                                                                                                                                       |
   +----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | disable  | Used to disable a specified table, for example, **disable 'test'**.                                                                                                                                                             |
   +----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | enable   | Used to enable a specified table, for example, **enable 'test'**.                                                                                                                                                               |
   +----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | alter    | Used to alter the table structure. You can run the **alter** command to add, modify, or delete column family information and table-related parameter values, for example, **alter 'test', {NAME => 'f3', METHOD => 'delete'}**. |
   +----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | describe | Used to obtain the table description, for example, **describe 'test'**.                                                                                                                                                         |
   +----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | drop     | Used to delete a specified table, for example, **drop 'test'**. Before deleting a table, you must stop it.                                                                                                                      |
   +----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | put      | Used to write the value of a specified cell, for example, **put 'test','r1','f1:c1','myvalue1'**. The cell location is unique and determined by the table, row, and column.                                                     |
   +----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | get      | Used to get the value of a row or the value of a specified cell in a row, for example, **get 'test','r1'**.                                                                                                                     |
   +----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | scan     | Used to query table data, for example, **scan 'test'**. The table name and scanner must be specified in the command.                                                                                                            |
   +----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
