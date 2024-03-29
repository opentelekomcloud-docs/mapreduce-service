:original_name: mrs_01_0952.html

.. _mrs_01_0952:

Using a Hive Client
===================

Scenario
--------

This section guides users to use a Hive client in an O&M or service scenario.

Prerequisites
-------------

-  The client has been installed. For example, the client is installed in the **/opt/hadoopclient** directory. The client directory in the following operations is only an example. Change it to the actual installation directory.
-  Service component users are created by the administrator as required. In security mode, machine-machine users need to download the keytab file. A human-machine user must change the password upon the first login.

Using the Hive Client
---------------------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to go to the client installation directory:

   **cd** **/opt/hadoopclient**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Log in to the Hive client based on the cluster authentication mode.

   -  In security mode, run the following command to complete user authentication and log in to the Hive client:

      **kinit** *Component service user*

      **beeline**

   -  In common mode, run the following command to log in to the Hive client. If no component service user is specified, the current OS user is used to log in to the Hive client.

      **beeline -n** *component service user*

#. Run the following command to execute the HCatalog client command:

   **hcat -e** *"cmd"*

   *cmd* must be a Hive DDL statement, for example, **hcat -e "show tables"**.

   .. note::

      -  To use the HCatalog client, choose **More** > **Download Client** on the service page to download the clients of all services. This restriction does not apply to the beeline client.

      -  Due to permission model incompatibility, tables created using the HCatalog client cannot be accessed on the HiveServer client. However, the tables can be accessed on the WebHCat client.

      -  If you use the HCatalog client in Normal mode, the system performs DDL commands using the current user who has logged in to the operating system.

      -  Exit the beeline client by running the **!q** command instead of by pressing **Ctrl + C**. Otherwise, the temporary files generated by the connection cannot be deleted and a large number of junk files will be generated as a result.

      -  If multiple statements need to be entered during the use of beeline clients, separate the statements from each other using semicolons (**;**) and set the value of **entireLineAsCommand** to **false**.

         Setting method: If beeline has not been started, run the **beeline --entireLineAsCommand=false** command. If the beeline has been started, run the **!set entireLineAsCommand false** command.

         After the setting, if a statement contains semicolons (**;**) that do not indicate the end of the statement, escape characters must be added, for example, **select concat_ws('\\;', collect_set(col1)) from tbl**.

Common Hive Client Commands
---------------------------

The following table lists common Hive Beeline commands.

For more commands, see https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-BeelineCommands.

.. table:: **Table 1** Common Hive Beeline commands

   +-----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Command                                                                                                   | Description                                                                                                                                                                                                                  |
   +===========================================================================================================+==============================================================================================================================================================================================================================+
   | set <key>=<value>                                                                                         | Sets the value of a specific configuration variable (key).                                                                                                                                                                   |
   |                                                                                                           |                                                                                                                                                                                                                              |
   |                                                                                                           | .. note::                                                                                                                                                                                                                    |
   |                                                                                                           |                                                                                                                                                                                                                              |
   |                                                                                                           |    If the variable name is incorrectly spelled, the Beeline does not display an error.                                                                                                                                       |
   +-----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | set                                                                                                       | Prints the list of configuration variables overwritten by users or Hive.                                                                                                                                                     |
   +-----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | set -v                                                                                                    | Prints all configuration variables of Hadoop and Hive.                                                                                                                                                                       |
   +-----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | add FILE[S] <filepath> <filepath>*add JAR[S] <filepath> <filepath>*add ARCHIVE[S] <filepath> <filepath>\* | Adds one or more files, JAR files, or ARCHIVE files to the resource list of the distributed cache.                                                                                                                           |
   +-----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | add FILE[S] <ivyurl> <ivyurl>\*                                                                           | Adds one or more files, JAR files, or ARCHIVE files to the resource list of the distributed cache using the lvy URL in the **ivy://goup:module:version?query_string** format.                                                |
   |                                                                                                           |                                                                                                                                                                                                                              |
   | add JAR[S] <ivyurl> <ivyurl>\*                                                                            |                                                                                                                                                                                                                              |
   |                                                                                                           |                                                                                                                                                                                                                              |
   | add ARCHIVE[S] <ivyurl> <ivyurl>\*                                                                        |                                                                                                                                                                                                                              |
   +-----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | list FILE[S]list JAR[S]list ARCHIVE[S]                                                                    | Lists the resources that have been added to the distributed cache.                                                                                                                                                           |
   +-----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | list FILE[S] <filepath>*list JAR[S] <filepath>*list ARCHIVE[S] <filepath>\*                               | Checks whether given resources have been added to the distributed cache.                                                                                                                                                     |
   +-----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | delete FILE[S] <filepath>*delete JAR[S] <filepath>*delete ARCHIVE[S] <filepath>\*                         | Deletes resources from the distributed cache.                                                                                                                                                                                |
   +-----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | delete FILE[S] <ivyurl> <ivyurl>\*                                                                        | Delete the resource added using **<ivyurl>** from the distributed cache.                                                                                                                                                     |
   |                                                                                                           |                                                                                                                                                                                                                              |
   | delete JAR[S] <ivyurl> <ivyurl>\*                                                                         |                                                                                                                                                                                                                              |
   |                                                                                                           |                                                                                                                                                                                                                              |
   | delete ARCHIVE[S] <ivyurl> <ivyurl>\*                                                                     |                                                                                                                                                                                                                              |
   +-----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | reload                                                                                                    | Enable HiveServer2 to discover the change of the JAR file **hive.reloadable.aux.jars.path** in the specified path. (You do not need to restart HiveServer2.) Change actions include adding, deleting, or updating JAR files. |
   +-----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | dfs <dfs command>                                                                                         | Runs the **dfs** command.                                                                                                                                                                                                    |
   +-----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | <query string>                                                                                            | Executes the Hive query and prints the result to the standard output.                                                                                                                                                        |
   +-----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
