:original_name: mrs_01_1816.html

.. _mrs_01_1816:

Submitting Other Jobs
=====================

Scenario
--------

In addition to Hive, Spark2x, and Loader jobs, MapReduce, Java, Shell, HDFS, SSH, SubWorkflow, Streaming, and scheduled jobs can be submitted using the Oozie client.

.. note::

   You are advised to download the latest client.

Prerequisites
-------------

-  The Oozie component and its client have been installed and are running properly.
-  You have created or obtained the human-machine account and password for accessing the Oozie service.

   .. note::

      -  Shell job:

         This user must belong to the **hadoop** and **supergroup** groups and be assigned the Oozie role operation permission. The Shell script must have the execution permission on each NodeManager.

      -  SSH job:

         This user must belong to the **hadoop** and **supergroup** groups and be assigned the Oozie role operation permission. The mutual trust configuration is complete.

      -  Other jobs:

         This user must belong to the **hadoop** and **supergroup** groups and be assigned the Oozie role operation permission and other required permissions.

      -  This user must also be assigned the **manager_viewer** role at least.

-  You have obtained the URL of the Oozie server (any instance) in the running state, for example, **https://10.1.130.10:21003/oozie**.
-  You have obtained the name of the Oozie server, for example, **10-1-130-10**.
-  You have obtained the IP address of the active Yarn ResourceManager, for example, **10.1.130.11**.

Procedure
---------

#. Log in to the node where the Oozie client is installed as the client installation user.

#. Run the following command to obtain the installation environment. In the command, **/opt/client/** indicates the client installation path.

   **source /opt/client/bigdata_env**

#. Check the cluster authentication mode.

   -  If the cluster is in security mode, run the **kinit** command to authenticate users.

      For example, the **oozieuser** user is authenticated using the following command:

      **kinit oozieuser**

   -  If the cluster is in normal mode, go to :ref:`4 <mrs_01_1816__en-us_topic_0000001173630940_lc7fe1634fbdc45b592872850a4bd9def>`.

#. .. _mrs_01_1816__en-us_topic_0000001173630940_lc7fe1634fbdc45b592872850a4bd9def:

   Go to the example directory based on the type of the task you submit.

   .. table:: **Table 1** List of example directories

      +-----------------+-----------------------------------------------------------------------------------+
      | Job Type        | Example Directory                                                                 |
      +=================+===================================================================================+
      | MapReduce job   | *Client installation directory*/Oozie/oozie-client-``*``/examples/apps/map-reduce |
      +-----------------+-----------------------------------------------------------------------------------+
      | Java job        | *Client installation directory*/Oozie/oozie-client-``*``/examples/apps/java-main  |
      +-----------------+-----------------------------------------------------------------------------------+
      | Shell job       | *Client installation directory*/Oozie/oozie-client-``*``/examples/apps/shell      |
      +-----------------+-----------------------------------------------------------------------------------+
      | Streaming job   | *Client installation directory*/Oozie/oozie-client-``*``/examples/apps/streaming  |
      +-----------------+-----------------------------------------------------------------------------------+
      | SubWorkflow job | *Client installation directory*/Oozie/oozie-client-``*``/examples/apps/subwf      |
      +-----------------+-----------------------------------------------------------------------------------+
      | SSH job         | *Client installation directory*/Oozie/oozie-client-``*``/examples/apps/ssh        |
      +-----------------+-----------------------------------------------------------------------------------+
      | Scheduled job   | *Client installation directory*/Oozie/oozie-client-``*``/examples/apps/cron       |
      +-----------------+-----------------------------------------------------------------------------------+

   .. note::

      The examples of other jobs contain HDFS job examples.

   :ref:`Table 2 <mrs_01_1816__en-us_topic_0000001173630940_t4569c24069cf4e6b908ce637a4b6af6d>` lists the files that you need to pay attention to in the example directory.

   .. _mrs_01_1816__en-us_topic_0000001173630940_t4569c24069cf4e6b908ce637a4b6af6d:

   .. table:: **Table 2** File description

      +-----------------+----------------------------------------------------------------------------------------------------------------------+
      | File            | Description                                                                                                          |
      +=================+======================================================================================================================+
      | job.properties  | Parameter definition file of a workflow                                                                              |
      +-----------------+----------------------------------------------------------------------------------------------------------------------+
      | workflow.xml    | Rule definition file of a workflow                                                                                   |
      +-----------------+----------------------------------------------------------------------------------------------------------------------+
      | lib             | Directory of the JAR file on which a workflow depends                                                                |
      +-----------------+----------------------------------------------------------------------------------------------------------------------+
      | coordinator.xml | Scheduled job configuration file which can be used to set a scheduled policy. The file is in the **cron** directory. |
      +-----------------+----------------------------------------------------------------------------------------------------------------------+
      | oozie_shell.sh  | Shell script file required for submitting shell jobs. The file is in the **shell** directory.                        |
      +-----------------+----------------------------------------------------------------------------------------------------------------------+

#. Run the following command to edit the **job.properties** file:

   **vi job.properties**

   Perform the following modifications:

   Change the value of **userName** to the name of the human-machine user who submits the job, for example, **userName=oozieuser**.

#. Run the **oozie job** command to run the workflow file:

   **oozie job -oozie https://**\ *Host name of the oozie role*\ **:21003/oozie -config** *File path of job.properties* **-run**

   Example:

   **oozie job -oozie https://10-1-130-10:21003/oozie -config**

   **/opt/client/Oozie/oozie-client-*/examples/apps/map-reduce/job.properties -run**

   .. note::

      -  The command parameters are described as follows:

         **-oozie** URL of the Oozie server that executes a job

         **-config** Workflow property file

         **-run** Executing a workflow

      -  If a job ID, for example, **job: 0000021-140222101051722-oozie-omm-W**, is displayed after the workflow file is executed, the job is successfully submitted. You can view the execution results on the Oozie management page.

         Log in to the Oozie web UI at **https**://*IP address of the Oozie role*\ **:21003/oozie** as user **oozieuser**.

         On the Oozie web UI, you can view the submitted workflow information based on the job ID in the table on the page.
