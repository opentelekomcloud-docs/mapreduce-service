:original_name: mrs_03_1082.html

.. _mrs_03_1082:

How Do I View the Hive Table Created by Another User?
=====================================================

Versions earlier than MRS 3.\ *x*:

#. Log in to MRS Manager and choose **System** > **Permission** > **Manage Role**.
#. Click **Create Role**, and set **Role Name** and **Description**.
#. In the **Permission** table, choose **Hive** > **Hive Read Write Privileges**.
#. In the database list, click the name of the database where the table created by user B is stored. The table is displayed.
#. In the **Permission** column of the table created by user B, select **SELECT**.
#. Click **OK**, and return to the **Role** page.
#. Choose **System** > **Manage User**. Locate the row containing user A, click **Modify** to bind the new role to user A, and click **OK**. After about 5 minutes, user A can access the table created by user B.

MRS 3.\ *x* or later:

#. Log in to FusionInsight Manager and choose **Cluster** > **Services**. On the page that is displayed, choose **Hive**. On the displayed page, choose **More**, and check whether **Enable Ranger** is grayed out.

   -  If yes, go to :ref:`9 <mrs_03_1082__li9406195118112>`.
   -  If no, perform :ref:`2 <mrs_03_1082__li1778559161211>` to :ref:`8 <mrs_03_1082__li74548548355>`.

#. .. _mrs_03_1082__li1778559161211:

   Log in to FusionInsight Manager and choose **System** > **Permission** > **Role**.

#. Click **Create Role**, and set **Role Name** and **Description**.

#. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Hive** > **Hive Read Write Privileges**.

#. In the database list, click the name of the database where the table created by user B is stored. The table is displayed.

#. In the **Permission** column of the table created by user B, select **Select**.

#. Click **OK**, and return to the **Role** page.

#. .. _mrs_03_1082__li74548548355:

   Choose **Permission** > **User**. On the **Local User** page that is displayed, locate the row containing user A, click **Modify** in the **Operation** column to bind the new role to user A, and click **OK**. After about 5 minutes, user A can access the table created by user B.

#. .. _mrs_03_1082__li9406195118112:

   Perform the following steps to add the Ranger access permission policy of Hive:

   a. Log in to FusionInsight Manager as a Hive administrator and choose **Cluster** > **Services**. On the page that is displayed, choose **Ranger**. On the displayed page, click the URL next to **Ranger WebUI** to go to the Ranger management page.
   b. On the home page, click the component plug-in name in the **HADOOP SQL** area, for example, **Hive**.
   c. On the **Access** tab page, click **Add New Policy** to add a Hive permission control policy.
   d. In the **Create Policy** dialog box that is displayed, set the following parameters:

      -  **Policy Name**: Enter a policy name, for example, **table_test_hive**.
      -  **database**: Enter or select the database where the table created by user B is stored, for example, **default**.
      -  **table**: Enter or select the table created by user B, for example, **test**.
      -  **column**: Enter and select a column, for example, **\***.
      -  In the **Allow Conditions** area, click **Select User**, select user A, click **Add Permissions**, and select **select**.
      -  Click **Add**.

#. Perform the following steps to add the Ranger access permission policy of HDFS:

   a. Log in to FusionInsight Manager as user **rangeradmin** and choose **Cluster** > **Services**. On the page that is displayed, choose **Ranger**. On the displayed page, click the URL next to **Ranger WebUI** to go to the Ranger management page.
   b. On the home page, click the component plug-in name in the **HDFS** area, for example, **hacluster**.
   c. Click **Add New Policy** to add a HDFS permission control policy.
   d. In the **Create Policy** dialog box that is displayed, set the following parameters:

      -  **Policy Name**: Enter a policy name, for example, **tablehdfs_test**.
      -  **Resource Path**: Set this parameter to the HDFS path where the table created by user B is stored, for example, **/user/hive/warehouse/**\ *Database name*\ **/**\ *Table name*.
      -  In the **Allow Conditions** area, select user A for **Select User**, click **Add Permissions** in the **Permissions** column, and select **Read** and **Execute**.
      -  Click **Add**.

#. View basic information about the policy in the policy list. After the policy takes effect, user A can view the table created by user B.
