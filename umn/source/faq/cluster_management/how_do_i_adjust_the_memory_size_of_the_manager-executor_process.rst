:original_name: mrs_03_1228.html

.. _mrs_03_1228:

How Do I Adjust the Memory Size of the manager-executor Process?
================================================================

Symptom
-------

The **manager-executor** process runs either on the Master1 or Master2 node in the MRS cluster in active/standby mode. This process is used to encapsulate the MRS management and control plane's operations on the MRS cluster, such as job submission, heartbeat reporting, certain alarm reporting, as well as cluster creation, scale-out, and scale-in. When you submit jobs on the MRS management and control plane, the Executor memory may become insufficient as the tasks increase or the number of concurrent tasks increases. As a result, the CPU usage is high and the Executor process experiences out-of-memory (OOM) errors.

Procedure
---------

#. Log in to either the Master1 or Master2 node as user **root** and run the following command to switch to user **omm**:

   **su - omm**

#. Run the following command to modify the **catalina.sh** script. Specifically, search for **JAVA_OPTS** in the script, find the configuration items similar to **JAVA_OPTS="-Xms1024m -Xmx4096m**, and change the values of the items to desired ones, and save the modification.

   **vim /opt/executor/bin/catalina.sh**

#. The **manager-executor** process only runs on either the Master1 or Master2 node in active/standby mode. Check whether it exists on the node before restarting it.

   a. Log in to the Master1 and Master2 nodes and run the following command to check whether the process exists. If any command output is displayed, the process exists.

      **ps -ef \| grep "/opt/executor" \| grep -v grep**

   b. Run the following command to restart the process:

      **sh /opt/executor/bin/shutdown.shsh** **/opt/executor/bin/startup.sh**
