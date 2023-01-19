:original_name: mrs_01_0139.html

.. _mrs_01_0139:

HDFS on Hue
===========

Hue provides the file browser function for users to use HDFS in GUI mode.

.. caution::

   The Hue page is used to view and analyze data such as files and tables. Do not perform high-risk management operations such as deleting objects on the page. If an operation is required, you are advised to perform the operation on each component after confirming that the operation has no impact on services. For example, you can use the HDFS client to perform operations on HDFS files and use the Hive client to perform operations on Hive tables.

How to Use File Browser
-----------------------

Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

Click |image1|. The **File Browser** page is displayed. You can perform the following operations:

-  Viewing files or directories

   By default, the directory and files in the directory of the login user are displayed. You can view **Name**, **Size**, **User**, **Group**,\ **Permission**, and **Date**.

   Click a file name to view the text information or binary data in the text file. The file content can be edited.

   If there are a large number of files and directories, you can enter keywords in the search text box to search for specific files or directories.

-  Creating files or directories

   Click **New** in the upper right corner. Choose **File** to create the file. Choose **Directory** to create a directory.

-  Managing files or directories

   Select the check box of a file or director, and click **Actions**. In the displayed menu, choose **Rename**, **Move**, **Copy**, and **Change permissions** to rename, move, copy, or change the file or directory permissions.

-  Uploading files

   Click **Upload** in the upper right corner and click **Select files** or drag the file to the window.

How to Use Storage Policies
---------------------------

.. note::

   If the value of Hue parameter **fs_defaultFS** is set to **viewfs://ClusterX**, the big data storage policy cannot be enabled.

**Storage policies on the Hue web UI are classified into the following two types:**

-  Static Storage Policies

   #. Current storage policy

      According to the access frequency and importance of documents in HDFS, specify a storage policy for an HDFS directory, such as ONE_SSD or ALL_SSD. The files in this directory can be migrated to the storage media.

   #. Current EC policy

      Specify EC policies for HDFS directories, such as RS-10-4-1024k and RS-3-2-1024k. .

-  Dynamic Storage Policies

   Set rules for an HDFS directory. The system can automatically change the storage policy, the number of file copies, migrate the file directory..

   Before configuring a dynamic storage policy on the Hue WebUI, you must set the CRON expressions for cold and hot data migration and start automatic cold and hot data migration on Manager.

   Operations:

   Change the value of **dfs.auto.data.mover.cron.expression** for NameNode of the HDFS service. For details, see :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.

   .. note::

      -  **dfs.auto.data.mover.cron.expression** indicates the CRON expression for checking whether HDFS data meets the dynamic storage policy rule. It is used to control the start time of data migration. The default value is **0 \* \* \* \***, indicating that the detection is performed on the hour. When the dynamic storage policy rule is met, cold and hot data migration tasks are executed on the hour.
      -  The default value of **dfs.auto.data.mover.enable** is **false**. This parameter value is valid only when **dfs.auto.data.mover.enable** is set to **true**.

   :ref:`Table 1 <mrs_01_0139__en-us_topic_0000001173949682_t91112612806f4a4593c025e032e333ff>` describes the expression for modifying this parameter. **\*** indicates consecutive time segments.

   .. _mrs_01_0139__en-us_topic_0000001173949682_t91112612806f4a4593c025e032e333ff:

   .. table:: **Table 1** Parameters in the execution expression

      ====== ===========================================================
      Column Description
      ====== ===========================================================
      1      Minute. The value ranges from 0 to 59.
      2      Hour. The value ranges from 0 to 23.
      3      Date. The value ranges from 1 to 31.
      4      Month. The value ranges from 1 to 12.
      5      Week. The value ranges from 0 to 6. **0** indicates Sunday.
      ====== ===========================================================

**To set storage policies on the web UI, perform the following operations:**

#. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`.

2. .. _mrs_01_0139__en-us_topic_0000001173949682_li0303144818353:

   On FusionInsight Manager, choose **System** > **Permission > Role** > **Create Role**.

   a. Set **Role Name**.
   b. In the **Configure Resource Permission** area, choose *Name of the desired cluster* > **Hue**, select **Storage Policy Admin**, and click **OK**. Then, grant the permission to the role.

3. .. _mrs_01_0139__en-us_topic_0000001173949682_lad19ed90dd11448a8fc79c41d59f7cb1:

   Choose **System** > **Permission** > **User Group** > **Create User Group**. Set **Group Name**, and click **Add** next to **Role**. On the displayed page, select the created role, click **OK** to add the role to the group, and click **OK**.

4. Choose **System** > **Permission** > **User** > **Create**.

   a. **Username**: Enter the name of the user to be added.
   b. Set **User Type** to **Human-machine**.
   c. Set **Password** and **Confirm Password** for logging in to the Hue web UI.
   d. Click **Add** next to **User Group**. On the page that is displayed, select the created user group in :ref:`3 <mrs_01_0139__en-us_topic_0000001173949682_lad19ed90dd11448a8fc79c41d59f7cb1>`, **supergroup**, **hadoop**, and **hive**, and click **OK**.
   e. Set **Primary Group** to **hive**.
   f. Click **Add** next to **Role**. On the page that is displayed, select the created role in :ref:`2 <mrs_01_0139__en-us_topic_0000001173949682_li0303144818353>` and the **System_administrator** role, and click **OK**.
   g. Click **OK**. The user is added successfully.

5. Access the Hue web UI as the created user. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

6. In the left navigation pane, click |image2|. The **File Browser** page is displayed.

7. Select the check box of a directory and choose **Action** on the top of the page. Choose **Storage policies**.

8. In the dialog box that is displayed, set a new storage policy and click **OK**.

   -  On the **Static Storage Policy** tab page, select a policy from the **New EC Policy** drop-down list box and click **Save**.

   -  On the **Dynamic Storage Policy** tab page, you can create, delete, or modify a dynamic storage policy. :ref:`Table 2 <mrs_01_0139__en-us_topic_0000001173949682_td571837c121649f3b7d9966840d79a91>` describes the parameters.

      .. _mrs_01_0139__en-us_topic_0000001173949682_td571837c121649f3b7d9966840d79a91:

      .. table:: **Table 2** Parameters of the dynamic storage policy

         +-----------+-------------------------+---------------------------------------------------------------------------------------------------------+
         | Category  | Parameter               | Description                                                                                             |
         +===========+=========================+=========================================================================================================+
         | Rule      | Last Access to File     | Indicates the time when the file is last accessed.                                                      |
         +-----------+-------------------------+---------------------------------------------------------------------------------------------------------+
         |           | Last File Modification  | Indicates the time when the file is last modified.                                                      |
         +-----------+-------------------------+---------------------------------------------------------------------------------------------------------+
         | Operation | Change Number of Copies | Indicates the number of file copies.                                                                    |
         +-----------+-------------------------+---------------------------------------------------------------------------------------------------------+
         |           | Modify Storage Policy   | Indicates that you can modify storage policies to the following: HOT, WARM, COLD, ONE_SSD, and ALL_SSD. |
         +-----------+-------------------------+---------------------------------------------------------------------------------------------------------+
         |           | Move to Directory       | Indicates that you can move the file to another directory.                                              |
         +-----------+-------------------------+---------------------------------------------------------------------------------------------------------+

      .. note::

         -  You need to consider whether the rules conflict with each other and whether the rules damage the system when setting rules.
         -  When a directory is configured with multiple rules and operations, the rule that is triggered first is located at the bottom of the rule/operation list, and the rules that are triggered later are placed from bottom to top to prevent repeated operations.
         -  The system checks whether the files under the directory specified by the dynamic storage policy meet the rules on an hourly basis. If the files meet the rules, the execution is triggered. Execution logs are recorded in the **/var/log/Bigdata/hdfs/nn/hadoop.log** directory of the active NameNode.

Typical Scenarios
-----------------

On the Hue page, view and edit HDFS files in text or binary mode as follows:

**Viewing a File**

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.
#. In the left navigation pane, click |image3|. The **File Browser** page is displayed.
#. Click the name of the file to be viewed.
#. Click **View as binary** to switch from the text mode to the binary mode. Click **View as file** to switch from the binary mode to the text mode.

**Editing a file**

5. Click **Edit File**. The file content can be edited.
6. Click **Save** or **Save As** to save the file.

.. |image1| image:: /_static/images/en-us_image_0000001296059940.png
.. |image2| image:: /_static/images/en-us_image_0000001349059785.png
.. |image3| image:: /_static/images/en-us_image_0000001349259241.png
