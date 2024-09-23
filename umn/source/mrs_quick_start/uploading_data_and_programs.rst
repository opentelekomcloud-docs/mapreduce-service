:original_name: mrs_01_0028.html

.. _mrs_01_0028:

Uploading Data and Programs
===========================

Through the **Files** tab page, you can create, delete, import, export, delete files in the analysis cluster.

Background
----------

MRS clusters process data from OBS or HDFS. OBS provides customers with the data storage capabilities that are massive, secure, reliable, and cost-effective. MRS can directly process data in OBS. You can browse, manage, and use data on the web page of the management console and OBS Client.

Importing Data
--------------

Currently, MRS can only import data from OBS to HDFS. The file upload rate decreases with the increase of the file size. This mode applies to scenarios where the data volume is small.

You can perform the following steps to import files and directories:

#. Log in to the MRS console.

#. Choose **Clusters > Active Clusters** and click the name of the cluster to be queried to enter the page displaying the cluster's information.

#. Click the **Files** tab to go to the file management page.

#. Select **HDFS File List**.

#. Go to the data storage directory, for example, **bd_app1**.

   The **bd_app1** directory is only an example. You can use any directory on the page or create a new one.

   The requirements for creating a folder are as follows:

   -  The folder name contains a maximum of 255 characters. The full path cannot exceed 1,023 characters.
   -  The folder name cannot be empty.
   -  The folder name cannot contain the following special characters::literal:`/:*?"<>|\\;&,'`!{}[]$%+`
   -  The value cannot start or end with a period (.).
   -  The spaces at the beginning and end are ignored.

#. Click **Import Data** and configure the HDFS and OBS paths correctly. When configuring the OBS or HDFS path, click **Browse**, select a file directory, and click **Yes**.

   -  OBS path

      -  The path must start with **obs://**. In MRS 1.7.2 or earlier, the value must start with **s3a://**.
      -  Files or programs encrypted by KMS cannot be imported.
      -  An empty folder cannot be imported.
      -  The directory and file name can contain letters, digits, hyphens (-), and underscores (_), but cannot contain the following special characters\ ``;|&>,<'$*?\``
      -  The directory and file name cannot start or end with a space, but can contain spaces between them.
      -  The OBS full path contains a maximum of 1,023 characters.

   -  HDFS path

      -  The path starts with **/user** by default.
      -  The directory and file name can contain letters, digits, hyphens (-), and underscores (_), but cannot contain the following special characters:``;|&>,<'$*?\:``
      -  The directory and file name cannot start or end with a space, but can contain spaces between them.
      -  The HDFS full path contains a maximum of 1,023 characters.
      -  The HDFS parent directory in **HDFS File List** is displayed in the **HDFS Path** text box by default.

#. Click **OK**.

   You can view the file upload progress on the **File Operation Records** tab page. MRS processes the data import operation as a DistCp job. You can also check whether the DistCp job is successfully executed on the **Jobs** tab page.

Exporting Data
--------------

After the data analysis and computing are completed, you can store the data in HDFS or export them to OBS.

You can perform the following steps to export files and directories:

#. Log in to the MRS console.

#. Choose **Clusters > Active Clusters** and click the name of the cluster to be queried to enter the page displaying the cluster's basic information.

#. Click the **Files** tab to go to the file management page.

#. Select **HDFS File List**.

#. Go to the data storage directory, for example, **bd_app1**.

#. Click **Export Data** and configure the OBS and HDFS paths. When configuring the OBS or HDFS path, click **Browse**, select a file directory, and click **Yes**.

   -  OBS path

      -  The path must start with **obs://**. In MRS 1.7.2 or earlier, the value must start with **s3a://**.
      -  The directory and file name can contain letters, digits, hyphens (-), and underscores (_), but cannot contain the following special characters\ ``;|&>,<'$*?\``
      -  The directory and file name cannot start or end with a space, but can contain spaces between them.
      -  The OBS full path contains a maximum of 1,023 characters.

   -  HDFS path

      -  The path starts with **/user** by default.
      -  The directory and file name can contain letters, digits, hyphens (-), and underscores (_), but cannot contain the following special characters:``;|&>,<'$*?\:``
      -  The directory and file name cannot start or end with a space, but can contain spaces between them.
      -  The HDFS full path contains a maximum of 1,023 characters.
      -  The HDFS parent directory in **HDFS File List** is displayed in the **HDFS Path** text box by default.

   .. note::

      When a folder is exported to OBS, a label file named **folder name_$folder$** is added to the OBS path. Ensure that the exported folder is not empty. If the exported folder is empty, OBS cannot display the folder and only generates a file named **folder name_$folder$**.

#. Click **OK**.

   You can view the file upload progress on the **File Operation Records** tab page. MRS processes the data export operation as a DistCp job. You can also check whether the DistCp job is successfully executed on the **Jobs** tab page.
