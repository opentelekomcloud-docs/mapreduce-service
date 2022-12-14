:original_name: mrs_01_0136.html

.. _mrs_01_0136:

Using File Browser on the Hue Web UI
====================================

Scenario
--------

Users can use the Hue web UI to manage files in HDFS.

.. caution::

   The Hue page is used to view and analyze data such as files and tables. Do not perform high-risk management operations such as deleting objects on the page. If an operation is required, you are advised to perform the operation on each component after confirming that the operation has no impact on services. For example, you can use the HDFS client to perform operations on HDFS files and use the Hive client to perform operations on Hive tables.

Accessing File Browser
----------------------

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

#. In the left navigation pane, click |image1|. The **File Browser** page is displayed.

   By default, the homepage of **File Browser** is the home directory of the current login user. On the displayed page, the following information about subdirectories for files in the directory is displayed:

   .. table:: **Table 1** HDFS file attributes

      ========== ========================================
      Attribute  Description
      ========== ========================================
      Name       Name of a directory or file
      Size       File size
      User       Owner of a directory or file
      Group      Group of a directory or file
      Permission Permission of a directory or file
      Date       Time when a directory or file is created
      ========== ========================================

#. In the search box, enter a keyword. The system automatically searches directories or files in the current directory.

#. Clear the search criteria. The system displays all directories or files.

Performing Actions
------------------

#. On the **File Browser** page, select one or more directories or files.
#. Click **Actions**. On the menu that is displayed, select an operation.

   -  **Rename**: renames a directory or file.
   -  **Move**: moves a file. In **Move to**, select a new directory and click **Move**.
   -  **Copy**: copies the selected files or directories.
   -  **Change permissions**: changes permission to access the selected directory or file.

      -  You can grant the owner, the group, or other users with the **Read**, **Write**, and **Execute** permissions.
      -  **Sticky**: indicates that only HDFS administrators, directory owners, and file owners can move files in the directory.
      -  **Recursive**: indicates that permission is granted to subdirectories recursively.

   -  **Storage policies**: indicates the policies for storing files or directories in HDFS.
   -  **Summary**: indicates that the HDFS storage information about the selected file or directory can be viewed.

Uploading User Files
--------------------

#. On the **File Browser** page, click **Upload**.
#. In the displayed dialog box for uploading files, click **Select files** or drag the file to the dialog box.

Creating a New File or Directory
--------------------------------

#. On the **File Browser** page, click **New**.
#. Select an operation.

   -  **File**: creates a file. Enter a file name and click **Create**.
   -  **Directory**: creates a directory. Enter a directory name and click **Create**.

Storage Policy Definition and Usage
-----------------------------------

.. note::

   If the value of Hue parameter **fs_defaultFS** is set to **viewfs://ClusterX**, the big data storage policy cannot be enabled.

#. Log in to FusionInsight Manager.

#. .. _mrs_01_0136__li279017394416:

   On FusionInsight Manager, choose **System** > **Permission > Manage Role** > **Create Role**.

   a. Set **Role Name**.
   b. In the **Configure Resource Permission** area, choose *Name of the desired cluster* > **Hue**, select **Storage Policy Admin**, and click **OK**. Then, grant the permission to the role.

#. .. _mrs_01_0136__li1531874419141:

   Choose **System** > **Permission** > **User Group** > **Create User Group**. Set **Group Name** and click **Select and Add Role** next to **Role**. On the displayed page, select the role created in :ref:`2 <mrs_01_0136__li279017394416>` and click **OK** to add the role to the group.

#. Choose **System** > **Permission** > **User** > **Create**.

   a. **Username**: Enter the name of the user to be added.
   b. Set **User Type** to **Human-machine**.
   c. Set **Password** and **Confirm Password** for logging in to the Hue web UI.
   d. Click **Add** next to **User Group**. On the page that is displayed, select the user group created in :ref:`3 <mrs_01_0136__li1531874419141>`, **supergroup**, **hadoop**, and **hive**, and click **OK**.
   e. Set **Primary Group** to **hive**.
   f. Click **Add** on the right of **Role**. On the page that is displayed, select the role created in :ref:`2 <mrs_01_0136__li279017394416>` and **System_administrator** role, and click **OK**.
   g. Click **OK**. The user is added successfully.

#. Access the Hue web UI as the created user. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

#. In the left navigation tree, click |image2|. The **File Browser** page is displayed.

#. Select the check box of the directory and click **Actions** on the top of the page. Choose **Storage policies**.

#. In the dialog box that is displayed, set a new storage policy and click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001296090492.png
.. |image2| image:: /_static/images/en-us_image_0000001349170229.png
