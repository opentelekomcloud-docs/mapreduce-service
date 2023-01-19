:original_name: mrs_01_1810.html

.. _mrs_01_1810:

Using the Oozie Client
======================

Scenario
--------

This section describes how to use the Oozie client in an O&M scenario or service scenario.

Prerequisites
-------------

-  The client has been installed. For example, the installation directory is **/opt/hadoopclient**. The client directory in the following operations is only an example. Change it to the actual installation directory.

-  Service component users are created by the administrator as required. In security mode, machine-machine users need to download the keytab file. A human-machine user must change the password upon the first login.


Using the Oozie Client
----------------------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to go to the client installation directory.

   **cd /opt/hadoopclient**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Check the cluster authentication mode.

   -  If the cluster is in security mode, run the following command to authenticate the user: *exampleUser* indicates the name of the user who submits tasks.

      **kinit** *exampleUser*

   -  If the cluster is in normal mode, go to :ref:`5 <mrs_01_1810__en-us_topic_0000001173789874_li1585491617519>`.

#. .. _mrs_01_1810__en-us_topic_0000001173789874_li1585491617519:

   Perform the following operations to configure Hue:

   a. Configure the Spark2x environment (skip this step if the Spark2x task is not involved):

      **hdfs dfs -put /opt/hadoopclient/Spark2x/spark/jars/*.jar /user/oozie/share/lib/spark2x/**

   b. Upload the Oozie configuration file and JAR package to HDFS.

      **hdfs dfs -mkdir /user/**\ *exampleUser*

      **hdfs dfs -put -f /opt/hadoopclient/Oozie/oozie-client-*/examples /user/**\ *exampleUser*/

      .. note::

         -  *exampleUser* indicates the name of the user who submits tasks.

         -  If the user who submits the task and other files except **job.properties** are not changed, client installation directory **/Oozie/oozie-client-*/examples** can be repeatedly used after being uploaded to HDFS.

         -  When the JAR package in the HDFS directory **/user/oozie/share** changes, you need to restart the Oozie service.

         -  Resolve the JAR file conflict between Spark and Yarn about Jetty.

            **hdfs dfs -rm -f /user/oozie/share/lib/spark/jetty-all-9.2.22.v20170606.jar**

         -  In normal mode, if **Permission denied** is displayed during the upload, run the following commands:

            **su - omm**

            **source /opt/hadoopclient/bigdata_env**

            **hdfs dfs -chmod -R 777 /user/oozie**

            **exit**
