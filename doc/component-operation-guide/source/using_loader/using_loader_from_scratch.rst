:original_name: mrs_01_1084.html

.. _mrs_01_1084:

Using Loader from Scratch
=========================

You can use Loader to import data from the SFTP server to HDFS.

This section applies to MRS clusters earlier than 3.\ *x*.

Prerequisites
-------------

-  You have prepared service data.
-  You have created an analysis cluster.

Procedure
---------

#. Access the Loader page.

   a. Access the cluster details page.

      -  For versions earlier than MRS 1.9.2, log in to MRS Manager and choose **Services**.
      -  For MRS 1.9.2 or later, click the cluster name on the MRS console and choose **Components**.

   b. Choose **Hue**. In **Hue Web UI** of **Hue Summary**, click **Hue (Active)**. The Hue web UI is displayed.

   c. Choose **Data Browsers** > **Sqoop**.

      The job management tab page is displayed by default on the Loader page.

#. On the Loader page, click **Manage links**.

#. .. _mrs_01_1084__li48883218306:

   Click **New link** and create **sftp-connector**. For details, see :ref:`File Server Link <mrs_01_0402__s73ada4f9d7e94890a00a2c7a90856ba6>`.

#. .. _mrs_01_1084__li14723052103216:

   Click **New link**, enter the link name, select **hdfs-connector**, and create **hdfs-connector**.

#. On the Loader page, click **Manage jobs**.

#. Click **New Job**.

#. In **Connection**, set parameters.

   a. In **Name**, enter a job name.
   b. Select the source link created in :ref:`3 <mrs_01_1084__li48883218306>` and the target link created in :ref:`4 <mrs_01_1084__li14723052103216>`.

#. In **From**, configure the job of the source link.

   For details, see :ref:`ftp-connector or sftp-connector <mrs_01_0404__s033d5edc10164032b9ea23d01081beae>`.

#. In **To**, configure the job of the target link.

   For details, see :ref:`hdfs-connector <mrs_01_0405__s0e7a49c2520c498aa9e3d9fa84325e2e>`.

#. In **Task Config**, set job running parameters.

   .. table:: **Table 1** Loader job running properties

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
      | Dirty Data Directory                 | Directory for saving dirty data. If you leave this parameter blank, dirty data will not be saved.                                                                      |
      +--------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **Save**.
