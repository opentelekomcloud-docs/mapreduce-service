:original_name: mrs_01_1662.html

.. _mrs_01_1662:

Creating an HDFS Role
=====================

Scenario
--------

This section describes how to create and configure an HDFS role on FusionInsight Manager. The HDFS role is granted the rights to read, write, and execute HDFS directories or files.

A user has the complete permission on the created HDFS directories or files, that is, the user can directly read data from and write data to as well as authorize others to access the HDFS directories or files.

.. note::

   -  This section applies to MRS 3.\ *x* or later clusters.
   -  An HDFS role can be created only in security mode.
   -  If the current component uses Ranger for permission control, HDFS policies must be configured based on Ranger for permission management. For details, see :ref:`Adding a Ranger Access Permission Policy for HDFS <mrs_01_1856>`.

Prerequisites
-------------

The system administrator has understood the service requirements.

Procedure
---------

#. Log in to FusionInsight Manager, and choose **System** > **Permission** > **Role**.

#. On the displayed page, click **Create Role** and fill in **Role Name** and **Description**.

#. Configure the resource permission. For details, see :ref:`Table 1 <mrs_01_1662__tc5a4f557e6144488a1ace112bb8db6ee>`.

   **File System**: HDFS directory and file permission

   Common HDFS directories are as follows:

   -  **flume**: Flume data storage directory

   -  **hbase**: HBase data storage directory

   -  **mr-history**: MapReduce task information storage directory

   -  **tmp**: temporary data storage directory

   -  **user**: user data storage directory

      .. _mrs_01_1662__tc5a4f557e6144488a1ace112bb8db6ee:

      .. table:: **Table 1** Setting a role

         +-------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
         | Task                                                                                                              | Operation                                                                                                                            |
         +===================================================================================================================+======================================================================================================================================+
         | Setting the HDFS administrator permission                                                                         | In the **Configure Resource Permission** area, choose *Name of the desired cluster* > HDFS, and select **Cluster Admin Operations**. |
         |                                                                                                                   |                                                                                                                                      |
         |                                                                                                                   | .. note::                                                                                                                            |
         |                                                                                                                   |                                                                                                                                      |
         |                                                                                                                   |    The setting takes effect after the HDFS service is restarted.                                                                     |
         +-------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
         | Setting the permission for users to check and recover HDFS                                                        | a. In the **Configure Resource Permission** area, choose *Name of the desired cluster* > HDFS > **File System**.                     |
         |                                                                                                                   | b. Locate the save path of specified directories or files on HDFS.                                                                   |
         |                                                                                                                   | c. In the **Permission** column of the specified directories or files, select **Read** and **Execute**.                              |
         +-------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
         | Setting the permission for users to read directories or files of other users                                      | a. In the **Configure Resource Permission** area, choose *Name of the desired cluster* > HDFS > **File System**.                     |
         |                                                                                                                   | b. Locate the save path of specified directories or files on HDFS.                                                                   |
         |                                                                                                                   | c. In the **Permission** column of the specified directories or files, select **Read** and **Execute**.                              |
         +-------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
         | Setting the permission for users to write data to files of other users                                            | a. In the **Configure Resource Permission** area, choose *Name of the desired cluster* > HDFS > **File System**.                     |
         |                                                                                                                   | b. Locate the save path of specified files on HDFS.                                                                                  |
         |                                                                                                                   | c. In the **Permission** column of the specified files, select **Write** and **Execute**.                                            |
         +-------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
         | Setting the permission for users to create or delete sub-files or sub-directories in the directory of other users | a. In the **Configure Resource Permission** area, choose *Name of the desired cluster* > HDFS > **File System**.                     |
         |                                                                                                                   | b. Locate the path where the specified directory is saved in the HDFS.                                                               |
         |                                                                                                                   | c. In the **Permission** column of the specified directories, select **Write** and **Execute**.                                      |
         +-------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
         | Setting the permission for users to execute directories or files of other users                                   | a. In the **Configure Resource Permission** area, choose *Name of the desired cluster* > HDFS > **File System**.                     |
         |                                                                                                                   | b. Locate the save path of specified directories or files on HDFS.                                                                   |
         |                                                                                                                   | c. In the **Permission** column of the specified directories or files, select **Execute**.                                           |
         +-------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
         | Setting the permission for allowing subdirectories to inherit all permissions of their parent directories         | a. In the **Configure Resource Permission** area, choose *Name of the desired cluster* > HDFS > **File System**.                     |
         |                                                                                                                   | b. Locate the save path of specified directories or files on HDFS.                                                                   |
         |                                                                                                                   | c. In the **Permission** column of the specified directories or files, select **Recursive**.                                         |
         +-------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**, and return to the **Role** page.
