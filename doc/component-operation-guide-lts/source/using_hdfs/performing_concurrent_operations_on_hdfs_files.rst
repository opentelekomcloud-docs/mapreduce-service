:original_name: mrs_01_1684.html

.. _mrs_01_1684:

Performing Concurrent Operations on HDFS Files
==============================================

Scenario
--------

Performing this operation can concurrently modify file and directory permissions and access control tools in a cluster.

Impact on the System
--------------------

Performing concurrent file modification operations in a cluster has adverse impacts on the cluster performance. Therefore, you are advised to do so when the cluster is idle.

Prerequisites
-------------

-  The HDFS client or clients including HDFS has been installed. For example, the installation directory is **/opt/client**.
-  Service component users are created by the administrator as required. In security mode, machine-machine users need to download the keytab file. A human-machine user needs to change the password upon the first login. (This operation is not required in normal mode.)

Procedure
---------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to go to the client installation directory:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If the cluster is in security mode, the user executing the DistCp command must belong to the **supergroup** group and run the following command to perform user authentication. In normal mode, user authentication is not required.

   **kinit** *Component service user*

#. Increase the JVM size of the client to prevent out of memory (OOM). (32 GB is recommended for 100 million files.)

   .. note::

      The HDFS client exits abnormally and the error message "java.lang.OutOfMemoryError" is displayed after the HDFS client command is executed.

      This problem occurs because the memory required for running the HDFS client exceeds the preset upper limit (128 MB by default). You can change the memory upper limit of the client by modifying **CLIENT_GC_OPTS** in *<Client installation path>*\ **/HDFS/component_env**. For example, if you want to set the upper limit to 1 GB, run the following command:

      CLIENT_GC_OPTS="-Xmx1G"

      After the modification, run the following command to make the modification take effect:

      **source** <*Client installation path*>/**/bigdata_env**

#. Run the concurrent commands shown in the following table.

   +----------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------+
   | Command                                                                                                        | Description                                                                                                               | Function                                                                   |
   +================================================================================================================+===========================================================================================================================+============================================================================+
   | hdfs quickcmds [-t threadsNumber] [-p principal] [-k keytab] -setrep <rep> <path> ...                          | **threadsNumber** indicates the number of concurrent threads. The default value is the number of vCPUs of the local host. | Used to concurrently set the number of copies of all files in a directory. |
   |                                                                                                                |                                                                                                                           |                                                                            |
   |                                                                                                                | **principal** indicates the Kerberos user.                                                                                |                                                                            |
   |                                                                                                                |                                                                                                                           |                                                                            |
   |                                                                                                                | **keytab** indicates the Keytab file.                                                                                     |                                                                            |
   |                                                                                                                |                                                                                                                           |                                                                            |
   |                                                                                                                | **rep** indicates the number of replicas.                                                                                 |                                                                            |
   |                                                                                                                |                                                                                                                           |                                                                            |
   |                                                                                                                | **path** indicates the HDFS directory.                                                                                    |                                                                            |
   +----------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------+
   | hdfs quickcmds [-t threadsNumber] [-p principal] [-k keytab] -chown [owner][:[group]] <path> ...               | **threadsNumber** indicates the number of concurrent threads. The default value is the number of vCPUs of the local host. | Used to concurrently set the owner group of all files in the directory.    |
   |                                                                                                                |                                                                                                                           |                                                                            |
   |                                                                                                                | **principal** indicates the Kerberos user.                                                                                |                                                                            |
   |                                                                                                                |                                                                                                                           |                                                                            |
   |                                                                                                                | **keytab** indicates the Keytab file.                                                                                     |                                                                            |
   |                                                                                                                |                                                                                                                           |                                                                            |
   |                                                                                                                | **owner** indicates the owner.                                                                                            |                                                                            |
   |                                                                                                                |                                                                                                                           |                                                                            |
   |                                                                                                                | **group** indicates the group to which the user belongs.                                                                  |                                                                            |
   |                                                                                                                |                                                                                                                           |                                                                            |
   |                                                                                                                | **path** indicates the HDFS directory.                                                                                    |                                                                            |
   +----------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------+
   | hdfs quickcmds [-t threadsNumber] [-p principal] [-k keytab] -chmod <mode> <path> ...                          | **threadsNumber** indicates the number of concurrent threads. The default value is the number of vCPUs of the local host. | Used to concurrently set permissions for all files in a directory.         |
   |                                                                                                                |                                                                                                                           |                                                                            |
   |                                                                                                                | **principal** indicates the Kerberos user.                                                                                |                                                                            |
   |                                                                                                                |                                                                                                                           |                                                                            |
   |                                                                                                                | **keytab** indicates the Keytab file.                                                                                     |                                                                            |
   |                                                                                                                |                                                                                                                           |                                                                            |
   |                                                                                                                | **mode** indicates the permission (for example, 754).                                                                     |                                                                            |
   |                                                                                                                |                                                                                                                           |                                                                            |
   |                                                                                                                | **path** indicates the HDFS directory.                                                                                    |                                                                            |
   +----------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------+
   | hdfs quickcmds [-t threadsNumber] [-p principal] [-k keytab] -setfacl [{-b|-k} {-m|-x } ``...]|[--``\ set ...] | **threadsNumber** indicates the number of concurrent threads. The default value is the number of vCPUs of the local host. | Used to concurrently set ACL information for all files in a directory.     |
   |                                                                                                                |                                                                                                                           |                                                                            |
   |                                                                                                                | **principal** indicates the Kerberos user.                                                                                |                                                                            |
   |                                                                                                                |                                                                                                                           |                                                                            |
   |                                                                                                                | **keytab** indicates the Keytab file.                                                                                     |                                                                            |
   |                                                                                                                |                                                                                                                           |                                                                            |
   |                                                                                                                | **acl_spec** indicates the ACL list separated by commas (,).                                                              |                                                                            |
   |                                                                                                                |                                                                                                                           |                                                                            |
   |                                                                                                                | **path** indicates the HDFS directory.                                                                                    |                                                                            |
   +----------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------+
