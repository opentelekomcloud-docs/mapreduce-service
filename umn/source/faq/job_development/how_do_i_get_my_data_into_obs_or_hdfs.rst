:original_name: mrs_03_1015.html

.. _mrs_03_1015:

How Do I Get My Data into OBS or HDFS?
======================================

MRS can process data in OBS and HDFS. You can get your data into OBS or HDFS as follows:

#. Upload local data to OBS.

   a. Log in to the OBS console.
   b. Create a parallel file system named **userdata** on OBS and create the **program**, **input**, **output**, and **log** folders in the file system.

      #. Choose **Parallel File System** > **Create Parallel File System**, and create a file system named **userdata**.
      #. In the OBS file system list, click the file system name **userdata**, choose **Files** > **Create Folder**, and create the **program**, **input**, **output**, and **log** folders.

   c. Upload data to the **userdata** file system.

      #. Go to the **program** folder and click **Upload File**.
      #. Click **add file** and select a user program.
      #. Click **Upload**.
      #. Upload the user data file to the **input** directory using the same method.

#. Import OBS data to HDFS.

   You can import OBS data to HDFS only when **Kerberos Authentication** is disabled and the cluster is running.

   a. Log in to the MRS console.

   b. Click the name of the cluster.

   c. On the page displayed, select the **Files** tab page and click **HDFS File List**.

   d. Select a data directory, for example, **bd_app1**.

      The **bd_app1** directory is only an example. You can use any directory on the page or create a new one.

   e. Click **Import Data** and click **Browse** to select an OBS path and an HDFS path.

   f. Click **OK**.

      You can view the file upload progress on the **File Operation Records** tab page.
