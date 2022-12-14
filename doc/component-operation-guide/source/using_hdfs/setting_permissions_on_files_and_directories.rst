:original_name: mrs_01_0807.html

.. _mrs_01_0807:

Setting Permissions on Files and Directories
============================================

Scenario
--------

HDFS allows users to modify the default permissions of files and directories. The default mask provided by the HDFS for creating file and directory permissions is **022**. If you have special requirements for the default permissions, you can set configuration items to change the default permissions.

Configuration Description
-------------------------

**Parameter portal:**

Go to the **All Configurations** page of HDFS and enter a parameter name in the search box by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.

.. table:: **Table 1** Parameter description

   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter                 | Description                                                                                                                                                                                      | Default Value         |
   +===========================+==================================================================================================================================================================================================+=======================+
   | fs.permissions.umask-mode | This **umask** value (user mask) is used when the user creates files and directories in the HDFS on the clients. This parameter is similar to the file permission mask on Linux.                 | 022                   |
   |                           |                                                                                                                                                                                                  |                       |
   |                           | The parameter value can be in octal or in symbolic, for example, **022** (octal, the same as **u=rwx,g=r-x,o=r-x** in symbolic), or **u=rwx,g=rwx,o=** (symbolic, the same as **007** in octal). |                       |
   |                           |                                                                                                                                                                                                  |                       |
   |                           | .. note::                                                                                                                                                                                        |                       |
   |                           |                                                                                                                                                                                                  |                       |
   |                           |    The octal mask is opposite to the actual permission value. You are advised to use the symbol notation to make the description clearer.                                                        |                       |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
