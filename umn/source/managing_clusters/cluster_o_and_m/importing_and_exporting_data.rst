:original_name: en-us_topic_0019489057.html

.. _en-us_topic_0019489057:

Importing and Exporting Data
============================

Through the **Files** tab page, you can create, delete, import, export, delete files in the analysis cluster. Currently, file creation is not supported. Streaming clusters do not support the file management function on the MRS GUI. In a cluster with Kerberos authentication enabled, to read or write the folders in the root directory, add a role that has the required permissions on the folders by referring to :ref:`Creating a Role <mrs_01_0343>`. Then, add the new role to the user group to which the user who submits the job belongs by referring to :ref:`Related Tasks <mrs_01_0344__s855da92cb75446818be082dff6e197f1>`.

Background
----------

Data sources processed by MRS are from OBS or HDFS. OBS is an object-based storage service that provides you with massive, secure, reliable, and cost-effective data storage capabilities. MRS can process data in OBS directly. You can view, manage, and use data by using the web page of the management control platform or OBS client. In addition, you can use REST APIs independently or integrate APIs to service applications to manage and access data.

Before creating jobs, upload the local data to OBS for MRS to compute and analyze. MRS allows exporting data from OBS to HDFS for computing and analyzing. After the data analysis and computing are completed, you can store the data in HDFS or export them to OBS. HDFS and OBS can also store the compressed data in the format of **bz2** or **gz**.

.. _en-us_topic_0019489057__section6302178417377:

Importing Data
--------------

Currently, MRS can only import data from OBS to HDFS. The file upload rate decreases with the increase of the file size. This mode applies to scenarios where the data volume is small.

You can perform the following steps to import files and directories:

#. Log in to the MRS console.

#. Click |image1| in the upper-left corner on the management console and select a region and project.

#. Choose **Clusters > Active Clusters** and click the name of the cluster to be queried to enter the page displaying the cluster's information.

#. Click the **Files** tab, and go to the file management page.

#. Select **HDFS File List**.

#. Go to the data storage directory, for example, **bd_app1**.

   The **bd_app1** directory is only an example. You can use any directory on the page or create a new one.

   The requirements for creating a folder are as follows:

   -  The folder name contains a maximum of 255 characters, and the full path cannot exceed 1,023 characters.
   -  The folder name cannot be empty.
   -  The folder name cannot contain the following special characters::literal:`/:*?"<>|\\;&,'`!{}[]$%+`
   -  The value cannot start or end with a period (.).
   -  The spaces at the beginning and end are ignored.

#. Click **Import Data** and configure the HDFS and OBS paths correctly. When configuring the OBS or HDFS path, click **Browse**, select a file directory, and click **Yes**.

   -  OBS path

      -  The path must start with **obs://**. MRS 1.7.2 or earlier: The value must start with **s3a://**.
      -  Files or programs encrypted by KMS cannot be imported.
      -  An empty folder cannot be imported.
      -  The directory and file name can contain letters, digits, hyphens (-), and underscores (_), but cannot contain the following special characters:``;|&>,<'$*?\``
      -  The directory and file name cannot start or end with a space, but can contain spaces between them.
      -  The OBS full path contains a maximum of 1,023 characters.

   -  HDFS path

      -  The path starts with **/user** by default.
      -  The directory and file name can contain letters, digits, hyphens (-), and underscores (_), but cannot contain the following special characters:``;|&>,<'$*?\``
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

#. Click |image2| in the upper-left corner on the management console and select a region and project.

#. Choose **Clusters > Active Clusters** and click the name of the cluster to be queried to enter the page displaying the cluster's basic information.

#. Click the **Files** tab, and the file management page is displayed.

#. Select **HDFS File List**.

#. Go to the data storage directory, for example, **bd_app1**.

#. Click **Export Data** and configure the OBS and HDFS paths. When configuring the OBS or HDFS path, click **Browse**, select a file directory, and click **Yes**.

   -  OBS path

      -  The path must start with **obs://**. MRS 1.7.2 or earlier: The value must start with **s3a://**.
      -  The directory and file name can contain letters, digits, hyphens (-), and underscores (_), but cannot contain the following special characters:``;|&>,<'$*?\``
      -  The directory and file name cannot start or end with a space, but can contain spaces between them.
      -  The OBS full path contains a maximum of 1,023 characters.

   -  HDFS path

      -  The path starts with **/user** by default.
      -  The directory and file name can contain letters, digits, hyphens (-), and underscores (_), but cannot contain the following special characters:``;|&>,<'$*?\``
      -  The directory and file name cannot start or end with a space, but can contain spaces between them.
      -  The HDFS full path contains a maximum of 1,023 characters.
      -  The HDFS parent directory in **HDFS File List** is displayed in the **HDFS Path** text box by default.

   .. note::

      When a folder is exported to OBS, a label file named **folder name_$folder$** is added to the OBS path. Ensure that the exported folder is not empty. If the exported folder is empty, OBS cannot display the folder and only generates a file named **folder name_$folder$**.

#. Click **OK**.

   You can view the file upload progress on the **File Operation Records** tab page. MRS processes the data export operation as a DistCp job. You can also check whether the DistCp job is successfully executed on the **Jobs** tab page.

Viewing Operation Logs
----------------------

When importing and exporting data on the MRS management console, you can choose **Files > File Operation Records** to view the data import and export progress.

:ref:`Table 1 <en-us_topic_0019489057__table59621065102929>` describes the parameters of the file operation record.

.. _en-us_topic_0019489057__table59621065102929:

.. table:: **Table 1** File operation record parameters

   +-----------------------------------+---------------------------------------------------+
   | Parameter                         | Description                                       |
   +===================================+===================================================+
   | Submitted                         | Start time of data import or export.              |
   +-----------------------------------+---------------------------------------------------+
   | Source Path                       | Source path of data.                              |
   |                                   |                                                   |
   |                                   | -  OBS path during data import.                   |
   |                                   | -  HDFS path during data export.                  |
   +-----------------------------------+---------------------------------------------------+
   | Target Path                       | Target path of data.                              |
   |                                   |                                                   |
   |                                   | -  HDFS path during data import.                  |
   |                                   | -  OBS path during data import.                   |
   +-----------------------------------+---------------------------------------------------+
   | Status                            | Status during data import or export.              |
   |                                   |                                                   |
   |                                   | -  Submitted                                      |
   |                                   | -  Accepted                                       |
   |                                   | -  Running                                        |
   |                                   | -  Completed                                      |
   |                                   | -  Terminated                                     |
   |                                   | -  Abnormal                                       |
   +-----------------------------------+---------------------------------------------------+
   | Duration (min)                    | Time of data import or export.                    |
   |                                   |                                                   |
   |                                   | The unit is minute.                               |
   +-----------------------------------+---------------------------------------------------+
   | Result                            | Result of data import or export.                  |
   |                                   |                                                   |
   |                                   | -  Successful                                     |
   |                                   | -  Failed                                         |
   |                                   | -  Killed                                         |
   |                                   | -  Undefined                                      |
   +-----------------------------------+---------------------------------------------------+
   | Operation                         | View Log: allows you to view file operation logs. |
   +-----------------------------------+---------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001296217736.png
.. |image2| image:: /_static/images/en-us_image_0000001295738308.png
