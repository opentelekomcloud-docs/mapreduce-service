:original_name: mrs_01_0373.html

.. _mrs_01_0373:

Using File Browser on the Hue Web UI
====================================

Scenario
--------

Users can use the Hue web UI to manage files in HDFS in a cluster.

For versions earlier than MRS 1.9.2, MRS clusters with Kerberos authentication enabled support this function.

.. caution::

   The Hue page is used to view and analyze data such as files and tables. Do not perform high-risk management operations such as deleting objects on the page. If an operation is required, you are advised to perform the operation on each component after confirming that the operation has no impact on services. For example, you can use the HDFS client to perform operations on HDFS files and use the Hive client to perform operations on Hive tables.

File Browser (File Browser)
---------------------------

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0370>`.

#. Click |image1|. The **File Browser** page is displayed.

   You can view the home directory of the current login user.

   On the **File Browser** page, the following information about subdirectories for files in the directory is displayed.

   .. table:: **Table 1** HDFS file attributes

      =============== ========================================
      Attribute       Description
      =============== ========================================
      **Name**        Name of a directory or file
      **Size**        File size
      **User**        Owner of a directory or file
      **Group**       Group of a directory or file
      **Permissions** Permission of a directory or file
      **Date**        Time when a directory or file is created
      =============== ========================================

#. In the search box, enter a keyword. The system automatically searches directories or files in the current directory.

#. Clear the search criteria. The system displays all directories or files.

Performing Actions
------------------

#. Click |image2| and select one or more directories or files.
#. Click **Actions**. On the menu that is displayed, select an operation.

   -  **Rename**: renames a directory or file.
   -  **Move**: moves a file. In **Move to**, select a new directory and click **Move**.
   -  **Copy**: copies the selected files or directories.
   -  **Change permissions**: changes permission to access the selected directory or file.

      -  You can grant the owner, the group, or other users with the **Read**, **Write**, and **Execute** permissions.
      -  **Sticky**: indicates that only HDFS administrators, directory owners, and file owners can move files in the directory.
      -  **Recursive**: indicates that permission is granted to subdirectories recursively.

   -  **Storage policies**: indicates the policies for storing files or directories in HDFS.
   -  **Summary**: indicates that you can view HDFS storage information about the selected file or directory.

Accessing Other Directories
---------------------------

#. Click the directory name, type a full path you want to access, for example, **/mr-history/tmp**, and press **Enter**.

   The current user must have permission to access other directories.

#. Click **Home** to go to the home directory.

#. Click **History**. The history records of directory access are displayed and the directories can be accessed again.

#. Click **Trash** to access the recycle bin of the current directory.

   Click **Empty Trash** to clean up the recycle bin.

Uploading User Files
--------------------

#. Click |image3| and click **Upload**.
#. Select an operation.

   -  **Files**: uploads user files to the current user.
   -  **Zip/Tgz/Bz2 file**: uploads a compressed file. In the dialog box that is displayed, click **Select ZIP, TGZ or BZ2 files** to select the compressed file to be uploaded. The system automatically decompresses the file in HDFS. Compressed files in **ZIP**, **TGZ**, and **BZ2** formats are supported.

Creating a New File or Directory
--------------------------------

#. Click |image4| and click **New**.
#. Select an operation.

   -  **File**: creates a file. Enter a file name and click **Create**.
   -  **Directory**: creates a directory. Enter a directory name and click **Create**.

Storage Policy Definition and Usage
-----------------------------------

.. note::

   If the value of Hue parameter **fs_defaultFS** is set to **viewfs://ClusterX**, the big data storage policy cannot be enabled.

#. Log in to MRS Manager.
#. On MRS Manager, choose **System** > **Permission > Manage Role** > **Create Role**.

   a. Set **Role Name**.
   b. Choose **Configure Resource Permission > Hue**, select **Storage Policy Admin**, and click **OK** to grant the storage policy administrator permission to the role.

#. Choose **System** > **Permission** > **Manage User Group** > **Create User Group**, set **Group Name**, and click **Select and Add Role** next to **Role**. On the displayed page, select the created role and click **OK** to add the role to the group.
#. Choose **System** > **Permission** > **Manage User** > **Create User**.

   a. Specify the **Username** of a user who can log in to the Hue web UI and has the **Storage Policy Admin** permission.
   b. Set **User Type** to **Human-machine**.
   c. Set **Password** and **Confirm Password** for logging in to the Hue web UI.
   d. Click **Select and Join User Group** next to **User Group**. On the page that is displayed, select the created user group, **supergroup**, **hadoop**, and **hive**, and click **OK**.
   e. Set **Primary Group** to **hive**.
   f. Click **Select and Add Role** on the right of **Assign Rights by Role**. On the Select snf page that is displayed, select the newly created role and the **System_administrator** role, and click **OK**.
   g. Click **OK**. The user is added successfully.

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0370>`.
#. Click |image5| in the upper right corner.
#. Select the check box of the directory and click **Action** on the upper part of the page. Then select **Storage policies**.
#. In the dialog box that is displayed, set a new storage policy and click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001349289521.png
.. |image2| image:: /_static/images/en-us_image_0000001349289525.png
.. |image3| image:: /_static/images/en-us_image_0000001295770424.png
.. |image4| image:: /_static/images/en-us_image_0000001349169945.png
.. |image5| image:: /_static/images/en-us_image_0000001296090208.png
