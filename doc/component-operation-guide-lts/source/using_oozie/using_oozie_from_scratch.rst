:original_name: mrs_01_1808.html

.. _mrs_01_1808:

Using Oozie from Scratch
========================

Oozie is an open-source workflow engine that is used to schedule and coordinate Hadoop jobs.

Oozie can be used to submit a wide array of jobs, such as Hive, Spark2x, Loader, MapReduce, Java, DistCp, Shell, HDFS, SSH, SubWorkflow, Streaming, and scheduled jobs.

This section describes how to use the Oozie client to submit a MapReduce job.

Prerequisites
-------------

The client has been installed. For example, the installation directory is **/opt/client**. The client directory in the following operations is only an example. Change it based on the actual installation directory onsite.

Procedure
---------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to go to the client installation directory. Assume that the client is installed in **/opt/client**.

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Check the cluster authentication mode.

   -  If the cluster is in security mode, run the following command to authenticate the user: *UserOozie* indicates the user who submits tasks.

      **kinit** *UserOozie*

   -  If the cluster is in normal mode, go to :ref:`5 <mrs_01_1808__en-us_topic_0000001173471274_li1803152871315>`.

#. .. _mrs_01_1808__en-us_topic_0000001173471274_li1803152871315:

   Upload the Oozie configuration file and JAR package to HDFS.

   **hdfs dfs -mkdir /user/**\ *UserOozie*

   **hdfs dfs -put -f /opt/client/Oozie/oozie-client-*/examples /user/**\ *UserOozie*/

   *UserOozie* indicates the user who submits tasks.

#. Run the following commands to modify the job execution configuration file:

   **cd /opt/client/Oozie/oozie-client-*/examples/apps/map-reduce/**

   **vi job.properties**

   .. code-block::

      nameNode=hdfs://hacluster
      resourceManager=10.64.35.161:8032 (10.64.35.161 is the service plane IP address of the Yarn resourceManager (active) node, and 8032 is the port number of yarn.resourcemanager.port)
      queueName=default
      examplesRoot=examples
      user.name=admin
      oozie.wf.application.path=${nameNode}/user/${user.name}/${examplesRoot}/apps/map-reduce# HDFS upload path
      outputDir=map-reduce
      oozie.wf.rerun.failnodes=true

#. Run the following command to execute the Oozie job:

   **oozie job -oozie https://**\ *Host name of the Oozie role*\ **:21003/oozie/ -config job.properties -run**

   .. code-block:: console

      [root@kwephispra44947 map-reduce]# oozie job -oozie https://kwephispra44948:21003/oozie/ -config job.properties -run
      ......
      job: 0000000-200730163829770-oozie-omm-W

#. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`.

#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Oozie**, click the hyperlink next to **Oozie WebUI** to go to the Oozie page, and view the task execution result on the Oozie web UI.


   .. figure:: /_static/images/en-us_image_0000001349139549.png
      :alt: **Figure 1** Task execution result

      **Figure 1** Task execution result
