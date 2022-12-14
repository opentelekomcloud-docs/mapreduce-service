:original_name: mrs_01_0406.html

.. _mrs_01_0406:

Managing Loader Jobs
====================

Scenario
--------

You can create, view, edit, and delete jobs on the Loader page.

This section applies to versions earlier than MRS 3.x.

Prerequisites
-------------

You have accessed the Loader page. For details, see :ref:`Loader Page <mrs_01_0401__s12f4baccf3914471bee631d0ca198278>`.

Creating a Job
--------------

#. On the Loader page, click **New job**.

#. In **Connection**, set parameters.

   a. In **Name**, enter a job name.

   b. In **From link** and **To link**, select links accordingly.

      After you select a link of a type, data is obtained from the specified source and saved to the destination.

      .. note::

         If no available link exists, click **Add a new link**.

#. In **From**, configure the job of the source link.

   For details, see :ref:`Source Link Configurations of Loader Jobs <mrs_01_0404>`.

#. In **To**, configure the job of the destination link.

   For details, see :ref:`Destination Link Configurations of Loader Jobs <mrs_01_0405>`.

#. Check whether a database link is selected in **To link**.

   Database links include:

   -  generic-jdbc-connector
   -  hbase-connector
   -  hive-connector

   If you set **To link** to a database link, you need to configure a mapping between service data and a field in the database table.

   -  If you set it to a database link, go to :ref:`6 <mrs_01_0406__l56f38eb013c549b2b70d8f3a750ea8c4>`.
   -  If you do not set it to a database link, go to :ref:`7 <mrs_01_0406__l8e55b33fad0b4b52b4919120d3ab7597>`.

#. .. _mrs_01_0406__l56f38eb013c549b2b70d8f3a750ea8c4:

   In **Field Mapping**, enter a field mapping. Then proceed to :ref:`7 <mrs_01_0406__l8e55b33fad0b4b52b4919120d3ab7597>`.

   **Field Mapping** specifies a mapping between each column of user data and a field in the database table.

   .. table:: **Table 1** **Field Mapping** properties

      +-------------------+-------------------------------------------------------------------------------------------------+
      | Parameter         | Description                                                                                     |
      +===================+=================================================================================================+
      | Column Num        | Field sequence of service data                                                                  |
      +-------------------+-------------------------------------------------------------------------------------------------+
      | Sample            | First row of sample values of service data                                                      |
      +-------------------+-------------------------------------------------------------------------------------------------+
      | Column Family     | When **To link** is **hbase-connector**, you can select a column family for storing data.       |
      +-------------------+-------------------------------------------------------------------------------------------------+
      | Destination Field | Field for storing data                                                                          |
      +-------------------+-------------------------------------------------------------------------------------------------+
      | Type              | Type of the field selected by the user                                                          |
      +-------------------+-------------------------------------------------------------------------------------------------+
      | Row Key           | When **To link** is **hbase-connector**, you need to select **Destination Field** as a row key. |
      +-------------------+-------------------------------------------------------------------------------------------------+

   .. note::

      If the value of **From** is a connector of a file type, for example, SFTP, FTP, OBS, and HDFS files, the value of **Field Mapping** is the first row of data in the file. Ensure that the first row of data is complete. Otherwise, the Loader job will not extract columns that are not mapped.

#. .. _mrs_01_0406__l8e55b33fad0b4b52b4919120d3ab7597:

   In **Task Config**, set job running parameters.

   .. table:: **Table 2** Loader job running properties

      +--------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                            | Description                                                                                                                                                            |
      +======================================+========================================================================================================================================================================+
      | Extractors                           | Number of Map tasks                                                                                                                                                    |
      +--------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Loaders                              | Number of Reduce tasks                                                                                                                                                 |
      |                                      |                                                                                                                                                                        |
      |                                      | This parameter is displayed only when the destination field is HBase or Hive.                                                                                          |
      +--------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Max. Error Records in a Single Shard | Error record threshold. If the number of error records of a single Map task exceeds the threshold, the task automatically stops and the obtained data is not returned. |
      |                                      |                                                                                                                                                                        |
      |                                      | .. note::                                                                                                                                                              |
      |                                      |                                                                                                                                                                        |
      |                                      |    Data is read and written in batches for **MYSQL** and **MPPDB** of **generic-jdbc-connector** by default. Errors are recorded once at most for each batch of data.  |
      +--------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Dirty Data Directory                 | Specifies the directory for saving dirty data. If you leave this parameter blank, dirty data will not be saved.                                                        |
      +--------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Save**.

Viewing a Job
-------------

#. Access the Loader page. The Loader job management page is displayed by default.

   -  If Kerberos authentication is enabled for the cluster, all jobs created by the current user are displayed by default and other users' jobs cannot be displayed.
   -  If Kerberos authentication is disabled for the cluster, all Loader jobs of the cluster are displayed.

#. In **Sqoop Jobs**, enter a job name to filter the job.
#. Click **Refresh** to obtain the latest job status.

Editing a Job
-------------

#. Access the Loader page. The Loader job management page is displayed by default.
#. Click the job name to go to the edit page.
#. Modify the job configuration parameters based on service requirements.
#. Click **Save**.

   .. note::

      Basic job operations in the navigation bar on the left are **Run**, **Copy**, **Delete**, **Disable**, **History Record**, and **Show Job JSON Definition**.

Deleting a Job
--------------

#. Access the Loader page.

#. In the row of the specified job, click |image1|.

   You can also select one or more jobs and click **Delete** Job in the upper right corner of the job list.

#. In the dialog box, click **Yes, delete it**.

   If the state of a Loader job is **Running**, the job fails to be deleted.

.. |image1| image:: /_static/images/en-us_image_0000001296090328.jpg
