:original_name: mrs_01_0635.html

.. _mrs_01_0635:

Using Presto to Dump Data in DLF
================================

Prerequisites
-------------

-  The Presto component has been installed in an MRS cluster.
-  You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)
-  You have the permission to operate the OBS file system. For details, see and .
-  The Presto permission has been configured. For details, see :ref:`Configuring Presto Permissions <mrs_01_0636>`.

.. _mrs_01_0635__section2028018713307:

Creating a Data Connection of the MRS PrestoSQL Type in DLF
-----------------------------------------------------------

#. In the left navigation pane of the DLF console, choose **Connection** > **Manage Connection**.

#. In the upper right corner of the page, click **Create Data Connection**.

#. Set parameters according to :ref:`Table 1 <mrs_01_0635__table487712591418>`.

   .. _mrs_01_0635__table487712591418:

   .. table:: **Table 1** Parameters for creating a data connection

      +----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter            | Description                                                                                                                                           |
      +======================+=======================================================================================================================================================+
      | Data Connection Type | Select **MRS PrestoSQL**.                                                                                                                             |
      +----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Data Connection Name | Name of the data connection to be created, which contains 1 to 100 characters and consists of only letters, digits, underscores (_), and hyphens (-). |
      +----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Cluster Name         | Name of the MRS cluster to which Presto belongs.                                                                                                      |
      +----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Test** to test connectivity of the data connection to be created. If the test passes, the data connection is created.

#. Click **OK**.

Creating and Executing SQL Scripts on the DLF Script Development Page
---------------------------------------------------------------------

.. caution::

   In this scenario, the query results dumped to OBS can be retained for a maximum of 10,000 times. If the number of query times exceeds 10,000, the historical query results are automatically aged based on the query time sequence. To prevent data loss, exercise caution when performing this operation.

#. In the left navigation pane of the DLF console, choose **Development** > **Develop Script**.
#. In the right pane, click **Create SQL Script** and select **Presto**.
#. In the upper right part of the editor, select the connection created in :ref:`Creating a Data Connection of the MRS PrestoSQL Type in DLF <mrs_01_0635__section2028018713307>` from the **Connection** drop-down list.
#. In the upper right part of the editor, select the schema from the **Schema** drop-down list box.
#. Enter one or more SQL statements in the editor. If you need to run a specified SQL statement separately, select the SQL statement before running it.
#. In the upper part of the editor, click **Execute**. After executing the SQL statement, view the execution history and result of the script in the lower part of the editor.

   .. note::

      -  Administrator operations are not supported. That is, all commands that can be executed only after the **set role admin** command is executed are not supported.
      -  Each statement is executed independently. Therefore, the statement with context settings (for example, **use**) does not take effect after being executed.
      -  When Presto authorization is enabled, the default permissions of various users are as follows:

         -  All users have the read/write permissions on the **mrs_reserved** database in Hive by default.
         -  All IAM users with the MRS CommonOperations, MRS FullAccess, MRS Administrator, and Tenant Administrator policies have read/write permission on the **default** database in Hive, and users with the MRS ReadOnlyAccess policy have read-only permission on the database.
         -  User **admin** of the cluster and IAM users with the MRS FullAccess, MRS Administrator, and Tenant Administrator policies have the **admin** role permission on the Hive database.
