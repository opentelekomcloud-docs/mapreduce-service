:original_name: mrs_01_248997.html

.. _mrs_01_248997:

Interconnecting Yarn with OBS
=============================

Interconnecting with OBS
------------------------

#. Log in to the node on which the Yarn client is installed as a client installation user.

#. Run the following command to switch to the client installation directory.

   **cd** *Client installation directory*

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If the cluster is in security mode, run the following command to authenticate the user. The user must have the read and write permissions on the OBS directory. Skip user authentication for normal clusters.

   **kinit** *User performing HDFS operations*

#. Explicitly add the OBS file system to be accessed in the Yarn command line.

   -  Access the OBS file system.

      **hdfs dfs -ls obs://**\ *OBS parallel file system name*\ **/**\ *Path*

   -  Create a directory in the OBS file system.

      **hdfs dfs -mkdir obs://**\ *OBS parallel file system name/hadoop1*

   -  Execute the Yarn task to access OBS.

      **yarn jar** *Client installation directory*\ **/HDFS/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-*.jar pi -Dmapreduce.job.hdfs-servers=NAMESERVICE -fs obs://**\ *OBS parallel file system name* **1 1**

   **NAMESERVICE** indicates the NameService in HDFS. The default value is **hdfs://hacluster**. If there are multiple NameServices, separate them with **,**.

   The following command is an example:

   **yarn jar /opt/hadoopclient/HDFS/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-*.jar pi -Dmapreduce.job.hdfs-servers=hdfs://hacluster -fs obs://bucketname** **1 1**

   -  Run the following command to write data to OBS:

      **yarn jar** *Client installation directory*\ **/HDFS/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-*.jar teragen 100 obs://**\ *OBS parallel file system name*\ **/hadoop1/teragen1**

   -  Run the following command to copy data from OBS to HDFS:

      **hadoop distcp** **obs://**\ *OBS parallel file system name*\ **/hadoop1/teragen1** **/tmp**

.. note::

   If a large number of logs are printed in the OBS file system, the read and write performance may be affected. You can adjust the log level of the OBS client as follows:

   **cd** *Client installation directory*\ **/Yarn/config**

   **vi log4j.properties**

   Add the OBS log level configuration to the file. (If an application uses the built-in **log4j.properties** file, add the same configuration.)

   **log4j.logger.org.apache.hadoop.fs.obs=WARN**

   **log4j.logger.com.obs=WARN**

   |image1|

Configuring Ranger Permissions
------------------------------

#. .. _mrs_01_248997__en-us_topic_0000001657144846_li468863917426:

   Log in to FusionInsight Manager and choose **System** > **Permission** > **User Group**. On the displayed page, click **Create User Group** to create a user group without any roles, for example, **obs_hadoop1**.

#. Back to FusionInsight Manager and choose **System** > **Permission** > **User**. On the displayed page, click **Create User** to create a user that is associated with the **obs_hadoop1** user group and the **default** role, for example, **hadoopuser1**.

#. Log in to the Ranger management page as the **rangeradmin** user.

#. On the home page, click component plug-in name **OBS** in the **EXTERNAL AUTHORIZATION** area.

#. Click **Add New Policy** and add the **Read** and **Write** permissions on the desired OBS paths to the user group created in :ref:`1 <mrs_01_248997__en-us_topic_0000001657144846_li468863917426>`.

   The following figure shows the configurations needed for adding the **Read** and **Write** permissions on **obs://**\ *OBS parallel file system name*\ **/hadoop1** to user group **obs_hadoop1**.

   |image2|

.. |image1| image:: /_static/images/en-us_image_0000002009454293.png
.. |image2| image:: /_static/images/en-us_image_0000001973053822.png
