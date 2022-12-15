:original_name: mrs_01_24188.html

.. _mrs_01_24188:

Using an HDFS Client
====================

Scenario
--------

This section describes how to use the HDFS client in an O&M scenario or service scenario.

Prerequisites
-------------

-  The client has been installed.

   For example, the installation directory is **/opt/hadoopclient**. The client directory in the following operations is only an example. Change it to the actual installation directory.

-  Service component users are created by the administrator as required. In security mode, machine-machine users need to download the keytab file. A human-machine user needs to change the password upon the first login. (This operation is not required in normal mode.)

Using the HDFS Client
---------------------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to go to the client installation directory:

   **cd /opt/hadoopclient**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If the cluster is in security mode, run the following command to authenticate the user. In normal mode, user authentication is not required.

   **kinit** *Component service user*

#. Run the HDFS Shell command. Example:

   **hdfs dfs -ls /**

Common HDFS Client Commands
---------------------------

The following table lists common HDFS client commands.

For more commands, see https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-common/CommandsManual.html#User_Commands.

.. table:: **Table 1** Common HDFS client commands

   +--------------------------------------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------------------------------------------+
   | Command                                                                        | Description                                                 | Example                                                                                 |
   +================================================================================+=============================================================+=========================================================================================+
   | **hdfs dfs -mkdir** *Folder name*                                              | Used to create a folder.                                    | **hdfs dfs -mkdir /tmp/mydir**                                                          |
   +--------------------------------------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------------------------------------------+
   | **hdfs dfs -ls** *Folder name*                                                 | Used to view a folder.                                      | **hdfs dfs -ls /tmp**                                                                   |
   +--------------------------------------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------------------------------------------+
   | **hdfs dfs -put** *Local file on the client node* *Specified HDFS path*        | Used to upload a local file to a specified HDFS path.       | **hdfs dfs -put /opt/test.txt /tmp**                                                    |
   |                                                                                |                                                             |                                                                                         |
   |                                                                                |                                                             | Upload the **/opt/test.txt** file on the client node to the **/tmp** directory of HDFS. |
   +--------------------------------------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------------------------------------------+
   | **hdfs dfs -get** *Specified file on HDFS* *Specified path on the client node* | Used to download the HDFS file to the specified local path. | **hdfs dfs -get /tmp/test.txt /opt/**                                                   |
   |                                                                                |                                                             |                                                                                         |
   |                                                                                |                                                             | Download the **/tmp/test.txt** file on HDFS to the **/opt** path on the client node.    |
   +--------------------------------------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------------------------------------------+
   | **hdfs dfs -rm -r -f** *Specified folder on HDFS*                              | Used to delete a folder.                                    | **hdfs dfs -rm -r -f /tmp/mydir**                                                       |
   +--------------------------------------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------------------------------------------+
   | **hdfs dfs -chmod** *Permission parameter File directory*                      | Used to configure the HDFS directory permission for a user. | **hdfs dfs -chmod 700 /tmp/test**                                                       |
   +--------------------------------------------------------------------------------+-------------------------------------------------------------+-----------------------------------------------------------------------------------------+

Client-related FAQs
-------------------

#. What do I do when the HDFS client exits abnormally and error message "java.lang.OutOfMemoryError" is displayed after the HDFS client command is running?

   This problem occurs because the memory required for running the HDFS client exceeds the preset upper limit (128 MB by default). You can change the memory upper limit of the client by modifying **CLIENT_GC_OPTS** in *<Client installation path>*\ **/HDFS/component_env**. For example, if you want to set the upper limit to 1 GB, run the following command:

   .. code-block::

      CLIENT_GC_OPTS="-Xmx1G"

   After the modification, run the following command to make the modification take effect:

   **source** <*Client installation path*>/**/bigdata_env**

#. How do I set the log level when the HDFS client is running?

   By default, the logs generated during the running of the HDFS client are printed to the console. The default log level is INFO. To enable the DEBUG log level for fault locating, run the following command to export an environment variable:

   **export HADOOP_ROOT_LOGGER=DEBUG,console**

   Then run the HDFS Shell command to generate the DEBUG logs.

   If you want to print INFO logs again, run the following command:

   **export HADOOP_ROOT_LOGGER=INFO,console**

#. How do I delete HDFS files permanently?

   HDFS provides a recycle bin mechanism. Typically, after an HDFS file is deleted, the file is moved to the recycle bin of HDFS. If the file is no longer needed and the storage space needs to be released, clear the corresponding recycle bin directory, for example, **hdfs://hacluster/user/xxx/.Trash/Current/**\ *xxx*.
