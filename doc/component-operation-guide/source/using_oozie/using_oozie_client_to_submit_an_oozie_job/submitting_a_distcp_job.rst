:original_name: mrs_01_2392.html

.. _mrs_01_2392:

Submitting a DistCp Job
=======================

Scenario
--------

This section describes how to submit a DistCp job using the Oozie client.

.. note::

   You are advised to download the latest client.

Prerequisites
-------------

-  The HDFS and Oozie components and clients have been installed and are running properly.

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

#. Log in to the node where the Oozie client is installed as the client installation user .

#. Run the following command to obtain the installation environment. **/opt/client/** is an example client installation path.

   **source /opt/client/bigdata_env**

#. Check the cluster authentication mode.

   -  If the cluster is in security mode, run the **kinit** command to authenticate users.

      For example, the **oozieuser** user is authenticated using the following command:

      **kinit oozieuser**

   -  If the cluster is in normal mode, go to :ref:`4 <mrs_01_2392__lcc62479277a945d99a305c3a8402a40d>`.

#. .. _mrs_01_2392__lcc62479277a945d99a305c3a8402a40d:

   Run the following command to go to the example directory:

   **cd /opt/client/Oozie/oozie-client-*/examples/apps/distcp/**

   :ref:`Table 1 <mrs_01_2392__ta1113e97d79c4106a91f5e20da6899e0>` lists the files that you need to pay attention to in the directory.

   .. _mrs_01_2392__ta1113e97d79c4106a91f5e20da6899e0:

   .. table:: **Table 1** File description

      ============== =======================================
      File           Description
      ============== =======================================
      job.properties Parameter definition file of a workflow
      workflow.xml   Rule definition file of a workflow
      ============== =======================================

#. Run the following command to edit the **job.properties** file:

   **vi job.properties**

   Perform the following modifications:

   Change the value of **userName** to the name of the human-machine user who submits the job, for example, **userName=oozieuser**.

#. Whether DistCp is not deployed across security clusters.

   -  If yes, go to :ref:`7 <mrs_01_2392__li57541420123918>`.
   -  If no, go to :ref:`9 <mrs_01_2392__lcabd43b3fb314898bc19ded29c90a2b3>`.

#. .. _mrs_01_2392__li57541420123918:

   Establish cross-Manager mutual trust between two clusters.

#. Run the following commands to back up and modify the **workflow.xml** file:

   **cp workflow.xml workflow.xml.bak**

   **vi workflow.xml**

   Modify the following content:

   .. code-block::

      <workflow-app xmlns="uri:oozie:workflow:1.0" name="distcp-wf">
          <start to="distcp-node"/>
          <action name="distcp-node">
              <distcp xmlns="uri:oozie:distcp-action:1.0">
                  <resource-manager>${resourceManager}</resource-manager>
                  <name-node>${nameNode}</name-node>
                  <prepare>
                      <delete path="hdfs://target_ip:target_port/user/${userName}/${examplesRoot}/output-data/${outputDir}"/>
                  </prepare>
                  <configuration>
                      <property>
                          <name>mapred.job.queue.name</name>
                          <value>${queueName}</value>
                      </property>
                      <property>
                          <name>oozie.launcher.mapreduce.job.hdfs-servers</name>
                          <value>hdfs://source_ip:source_port,hdfs://target_ip:target_port</value>
                      </property>
                  </configuration>
                  <arg>${nameNode}/user/${userName}/${examplesRoot}/input-data/text/data.txt</arg>
                  <arg>hdfs://target_ip:target_port/user/${userName}/${examplesRoot}/output-data/${outputDir}/data.txt</arg>
                  </distcp>
              <ok to="end"/>
              <error to="fail"/>
          </action>
          <kill name="fail">
              <message>DistCP failed, error message[${wf:errorMessage(wf:lastErrorNode())}]</message>
          </kill>
          <end name="end"/>
      </workflow-app>

   **target_ip:target_port** is the HDFS active NameNode address of the other trusted cluster, for example, **10.10.10.233:25000**.

   **source_ip:source_port** indicates the HDFS active NameNode address of the source cluster, for example, **10.10.10.223:25000**.

   Change the two IP addresses and port numbers based on the site requirements.

#. .. _mrs_01_2392__lcabd43b3fb314898bc19ded29c90a2b3:

   Run the **oozie job** command to run the workflow file:

   **oozie job -oozie https://**\ *Host name of the Oozie role*\ **:21003/oozie/ -config job.properties -run**

   .. note::

      -  The command parameters are described as follows:

         **-oozie** URL of the Oozie server that executes a job

         **-config** Workflow property file

         **-run** Executing a workflow

      -  If a job ID, for example, **job: 0000021-140222101051722-oozie-omm-W**, is displayed after the workflow file is executed, the job is successfully submitted. You can view the execution results on the Oozie management page.

         Log in to the Oozie web UI at **https**://*IP address of the Oozie role*\ **:21003/oozie** as user **oozieuser**.

         On the Oozie web UI, you can view the submitted workflow information based on the job ID in the table on the page.
