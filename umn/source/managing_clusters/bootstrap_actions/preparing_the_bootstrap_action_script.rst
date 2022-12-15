:original_name: mrs_01_0417.html

.. _mrs_01_0417:

Preparing the Bootstrap Action Script
=====================================

Currently, bootstrap actions support Linux shell scripts only. Script files must end with **.sh**.

Uploading the Installation Packages and Files to an OBS File System
-------------------------------------------------------------------

Before compiling a script, you need to upload all required installation packages, configuration packages, and relevant files to the OBS file system in the same region. Because networks of different regions are isolated from each other, MRS VMs cannot download OBS files from other regions.

Compiling a Script for Downloading Files from the OBS File System
-----------------------------------------------------------------

You can specify the file to be downloaded from OBS in the script. If you upload files to a private file system, you need to run the **hadoop fs** command to download the files. The following example shows that the **obs://yourbucket/myfile.tar.gz** file will be downloaded to the local host and decompressed to the **/your-dir** directory.

.. code-block:: text

   #!/bin/bash
   source /opt/Bigdata/client/bigdata_env;hadoop fs -D fs.obs.endpoint=<obs-endpoint> -D fs.obs.access.key=<your-ak> -D fs.obs.secret.key=<your-sk> -copyToLocal obs://yourbucket/myfile.tar.gz ./
   mkdir -p /<your-dir>
   tar -zxvf myfile.tar.gz -C /<your-dir>

.. note::

   -  In MRS 3.x and later versions, the default installation path of the client is /opt/Bigdata/client. In MRS 3.x and earlier versions, the default installation path is /opt/client. For details, see the actual situation.
   -  The Hadoop client has been preinstalled on the MRS node. You can run the **hadoop fs** command to download or upload data from or to OBS.
   -  Obtain the obs-endpoint of each region. For details, see `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__.
   -  :ref:`Sample Scripts <mrs_01_0418>` shows that the installation packages have been uploaded to the public readable OBS file system. Therefore, you can run the **curl** command in the sample script to download the installation packages.

Uploading the Script to the OBS File System
-------------------------------------------

After script compilation, upload the script to the OBS file system in the same region. At the time you specify, each node in the cluster downloads the script from OBS and executes the script as user **root**.
