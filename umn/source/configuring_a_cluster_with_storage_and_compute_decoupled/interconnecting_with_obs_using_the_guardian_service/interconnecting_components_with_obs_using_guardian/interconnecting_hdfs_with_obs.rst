:original_name: mrs_01_248996.html

.. _mrs_01_248996:

Interconnecting HDFS with OBS
=============================

Interconnecting with OBS
------------------------

#. Log in to the node on which the HDFS client is installed as a client installation user.

#. Run the following command to switch to the client installation directory:

   **cd** *Client installation directory*

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If the cluster is in security mode, run the following command to authenticate the user. The user must have the read and write permissions on the OBS directory. Skip user authentication for normal clusters.

   **kinit** *User performing HDFS operations*

#. Explicitly add the OBS file system to be accessed in the HDFS command line.

   The following commands are examples.

   -  Access the OBS file system.

      **hdfs dfs -ls obs://**\ *OBS parallel file system name*/*Path*

   -  Create a directory in the OBS file system.

      **hdfs dfs -mkdir obs://**\ *OBS parallel file system name/hadoop*

   -  Upload the **/opt/test.txt** file on the client node to the **obs://**\ *OBS parallel file system name*\ **/hadoop** directory.

      **hdfs dfs -put /opt/test.txt obs://**\ *OBS parallel file system name*\ **/hadoop**

.. note::

   If a large number of logs are printed in the OBS file system, the read and write performance may be affected. You can adjust the log level of the OBS client as follows:

   **cd** *Client installation directory*\ **/HDFS/hadoop/etc/hadoop**

   **vi log4j.properties**

   Add the OBS log level configuration to the file as follows:

   **log4j.logger.org.apache.hadoop.fs.obs=WARN**

   **log4j.logger.com.obs=WARN**

   |image1|

Configuring Ranger Permissions
------------------------------

#. Log in to FusionInsight Manager and choose **System** > **Permission** > **User Group**. On the displayed page, click **Create User Group** to create a user group without any roles, for example, **obs_hadoop**.

#. Back to FusionInsight Manager and choose **System** > **Permission** > **User**. On the displayed page, click **Create User** to create a user that is associated only with the **obs_hadoop** user group, for example, **hadoopuser**.

#. Log in to the Ranger management page as the **rangeradmin** user.

#. On the home page, click component plug-in name **OBS** in the **EXTERNAL AUTHORIZATION** area.

#. Click **Add New Policy** and add the **Read** and **Write** permissions on the desired OBS paths to the created user group.

   The following figure shows the configurations needed for adding the **Read** and **Write** permissions on **obs://**\ *OBS parallel file system name*\ **/hadoop** to user group **obs_hadoop**.

   |image2|

.. |image1| image:: /_static/images/en-us_image_0000001973053810.png
.. |image2| image:: /_static/images/en-us_image_0000001972894062.png
