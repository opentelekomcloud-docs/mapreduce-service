:original_name: mrs_01_1814.html

.. _mrs_01_1814:

Submitting a Spark2x Job
========================

Scenario
--------

This section describes how to submit a Spark2x job using the Oozie client.

.. note::

   You are advised to download the latest client.

Prerequisites
-------------

-  The Spark2x and Oozie components and clients have been installed and are running properly.

   If the current client is an earlier version, you need to download and install the client again.

-  You have created or obtained the human-machine account and password for accessing the Oozie service.

   .. note::

      -  This user must belong to the **hadoop**, **supergroup**, and **hive** groups and be assigned with the Oozie role operation permission. If the multi-instance function is enabled for Hive, the user must belong to a specific Hive instance group, for example, **hive3**.
      -  This user must also be assigned the **manager_viewer** role at least.

-  You have obtained the URL of the Oozie server (any instance) in the running state, for example, **https://10.1.130.10:21003/oozie**.
-  You have obtained the name of the Oozie server, for example, **10-1-130-10**.
-  You have obtained the IP address of the active Yarn ResourceManager, for example, **10.1.130.11**.

Procedure
---------

#. Log in to the node where the Oozie client is installed as the client installation user.

#. Run the following command to obtain the installation environment. **/opt/client/** is an example client installation path.

   **source /opt/client/bigdata_env**

#. Check the cluster authentication mode.

   -  If the cluster is in security mode, run the **kinit** command to authenticate users.

      For example, the **oozieuser** user is authenticated using the following command:

      **kinit oozieuser**

   -  If the cluster is in normal mode, go to :ref:`4 <mrs_01_1814__lcc62479277a945d99a305c3a8402a40d>`.

#. .. _mrs_01_1814__lcc62479277a945d99a305c3a8402a40d:

   Run the following command to go to the example directory:

   **cd /opt/client/Oozie/oozie-client-*/examples/apps/spark2x/**

   :ref:`Table 1 <mrs_01_1814__ta1113e97d79c4106a91f5e20da6899e0>` lists the files that you need to pay attention to in the directory.

   .. _mrs_01_1814__ta1113e97d79c4106a91f5e20da6899e0:

   .. table:: **Table 1** File description

      ============== =====================================================
      File           Description
      ============== =====================================================
      job.properties Parameter definition file of a workflow
      workflow.xml   Rule definition file of a workflow
      lib            Directory of the JAR file on which a workflow depends
      ============== =====================================================

#. Run the following command to edit the **job.properties** file:

   **vi job.properties**

   Perform the following modifications:

   Change the value of **userName** to the name of the human-machine user who submits the job, for example, **userName=oozieuser**.

#. Run the **oozie job** command to run the workflow file:

   **oozie job -oozie https://**\ *Host name of the Oozie role*\ **:21003/oozie/ -config job.properties -run**

   .. note::

      -  The command parameters are described as follows:

         **-oozie** URL of the Oozie server that executes a job

         **-config** Workflow property file

         **-run** Executing a workflow

      -  If a job ID, for example, **job: 0000021-140222101051722-oozie-omm-W**, is displayed after the workflow file is executed, the job is successfully submitted. You can view the execution results on the Oozie management page.

         Log in to the Oozie web UI at **https**://*IP address of the Oozie role*\ **:21003/oozie** as user **oozieuser**.

         On the Oozie web UI, you can view the submitted workflow information based on the job ID in the table on the page.
