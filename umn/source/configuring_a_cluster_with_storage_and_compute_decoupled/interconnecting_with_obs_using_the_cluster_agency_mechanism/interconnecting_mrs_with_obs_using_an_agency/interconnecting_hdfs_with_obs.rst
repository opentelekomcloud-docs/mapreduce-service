:original_name: mrs_01_1292.html

.. _mrs_01_1292:

Interconnecting HDFS with OBS
=============================

Before performing the following operations, ensure that you have configured a storage-compute decoupled cluster by referring to :ref:`Configuring a Storage-Compute Decoupled Cluster (Agency) <mrs_01_0768>` or :ref:`Configuring a Storage-Compute Decoupled Cluster (AK/SK) <mrs_01_0468>`.

#. Log in to the node on which the HDFS client is installed as a client installation user.

#. Run the following command to switch to the client installation directory.

   **cd ${client_home}**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If the cluster is in security mode, run the following command to authenticate the user. In normal mode, skip user authentication.

   **kinit** *Component service user*

#. Explicitly add the OBS file system to be accessed in the HDFS command line.

   Example:

   -  Run the following command to access the OBS file system:

      **hdfs dfs -ls obs://**\ *OBS parallel file system name*/*Path*

   -  Run the following command to upload the **/opt/test.txt** file from the client node to the OBS file system path:

      **hdfs dfs -put /opt/test.txt obs://**\ *OBS parallel file system name/Path*

.. note::

   If a large number of logs are printed in the OBS file system, the read and write performance may be affected. You can adjust the log level of the OBS client as follows:

   **cd ${client_home}/HDFS/hadoop/etc/hadoop**

   **vi log4j.properties**

   Add the OBS log level configuration to the file as follows:

   **log4j.logger.org.apache.hadoop.fs.obs=WARN**

   **log4j.logger.com.obs=WARN**

   |image1|

.. |image1| image:: /_static/images/en-us_image_0000001349257293.png
