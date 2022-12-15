:original_name: mrs_01_0408.html

.. _mrs_01_0408:

Example: Using Loader to Import Data from OBS to HDFS
=====================================================

Scenario
--------

If you need to import a large volume of data from the external cluster to the internal cluster, import it from OBS to HDFS.

Prerequisites
-------------

-  You have prepared service data.
-  You have created an analysis cluster.

Procedure
---------

#. Upload service data to your OBS file system.

#. Obtain the AK/SK information and create an OBS and HDFS link.

   For details, see :ref:`Loader Link Configuration <mrs_01_0402>`.

#. Access the Loader page.

   If Kerberos authentication is enabled in the analysis cluster, refer to instructions in :ref:`Accessing the Hue Web UI <mrs_01_0370>`.

#. Click **New Job**.

#. In **Information**, set parameters.

   a. In **Name**, enter a job name. For example, **obs2hdfs**.
   b. In **From link**, select the OBS link you create.
   c. In **To link**, select the HDFS link you create.

#. In **From**, set source link parameters.

   a. In **Bucket Name**, enter a name of the OBS file system.

   b. In **Input directory or file**, enter a detailed location of service data in the file system.

      If it is a single file, enter a complete path containing the file name. If it is a directory, enter the complete path of the directory.

   c. .. _mrs_01_0408__ld408930f2f5d426289bd0acd45f8e485:

      In **File format**, enter the type of the service data file.

   For details, see :ref:`obs-connector <mrs_01_0404__sdd455438f59c455d868736ad52d1097c>`.

#. In **To**, set destination link parameters.

   a. In **Output directory**, enter the directory for storing service data in HDFS.

      If Kerberos authentication is enabled in the cluster, the current user accessing Loader needs to have the permission to write data to the directory.

   b. In **File format**, enter the type of the service data file.

      The type must correspond to the type in :ref:`6.c <mrs_01_0408__ld408930f2f5d426289bd0acd45f8e485>`.

   c. In **Compression codec**, enter a compression algorithm. For example, if you do not compress data, select **NONE**.

   d. In **Overwrite**, select **True**.

   e. Click **Show Senior Parameter** and set **Line Separator**.

   f. Set **Field Separator**.

   For details, see :ref:`hdfs-connector <mrs_01_0405__s0e7a49c2520c498aa9e3d9fa84325e2e>`.

#. In **Task Config**, set job running parameters.

   a. In **Extractors**, enter the number of Map tasks.

   b. In **Loaders**, enter the number of Reduce tasks.

      If the destination link is an HDFS link, **Loaders** is hidden.

   c. In **Max error records in single split**, enter an error record threshold.

   d. In **Dirty data directory**, enter a directory for saving dirty data, for example, **/user/sqoop/obs2hdfs-dd**.

#. Click **Save and execute**.

   On the **Manage jobs** page, view the job running result. You can click **Refresh** to obtain the latest job status.
