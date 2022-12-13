:original_name: mrs_01_0294.html

.. _mrs_01_0294:

OMS Health Check Indicators
===========================

OMS Status Check
----------------

**Indicator**: OMS Status Check

**Description**: The OMS status check includes the HA status check and resource status check. The HA status includes **active**, **standby**, and **NULL**, indicating the active node, standby node, and unknown, respectively. The resource status includes normal, abnormal, and NULL. If the HA status is NULL, the HA status is unhealthy. If the resource status is NULL or abnormal, the resource status is unhealthy.

.. table:: **Table 1** OMS status description

   +-----------------------------------+--------------------------------------------------------+
   | Name                              | Description                                            |
   +===================================+========================================================+
   | HA state                          | **active**: indicates the active node.                 |
   |                                   |                                                        |
   |                                   | **standby**: indicates the standby node.               |
   |                                   |                                                        |
   |                                   | **NULL**: unknown                                      |
   +-----------------------------------+--------------------------------------------------------+
   | Resource status                   | **normal**: All resources are normal.                  |
   |                                   |                                                        |
   |                                   | **abnormal**: indicates that abnormal resources exist. |
   |                                   |                                                        |
   |                                   | **NULL**: unknown                                      |
   +-----------------------------------+--------------------------------------------------------+

**Recovery Guide**:

#. Log in to the active management node and run the **su - omm** command to switch to user **omm**. Run the **${CONTROLLER_HOME}/sbin/status-oms.sh** command to check the status of OMS.
#. If the HA status is NULL, the system may be restarting. NULL is an intermediate state, and the HA status will automatically change to a normal state.
#. If the resource status is abnormal, certain component resources of FusionInsight Manager are abnormal. Check whether the status of components such as acs, aos cep, controller, feed_watchdog, fms, guassDB, httpd, iam, ntp, okerberos, oldap, pms, and tomcat component is normal.
#. If any Manager component resource is abnormal, see Manager component status check to rectify the fault.

Manager Component Status Check
------------------------------

**Indicator**: Manager Component Status Check

**Description**: This indicator is used to check the running status and HA status of Manager components. The resource running status includes **Normal** and **Abnormal**, and the resource HA status includes **Normal** and **Exception**. Manager components include Acs, Aos, Cep, Controller, feed_watchdog, Floatip, Fms, GaussDB, HeartBeatCheck, httpd, IAM, NTP, Okerberos, OLDAP, PMS, and Tomcat. If the running status and HA status is not Normal, the check result is unhealthy.

.. table:: **Table 2** Manager status description

   +-----------------------------------+-----------------------------------------------------------------------+
   | Name                              | Description                                                           |
   +===================================+=======================================================================+
   | Resource running status:          | **Normal**: The system is running properly.                           |
   |                                   |                                                                       |
   |                                   | **Abnormal**: The running is abnormal.                                |
   |                                   |                                                                       |
   |                                   | **Stopped**: The task is stopped.                                     |
   |                                   |                                                                       |
   |                                   | **Unknown**: The status is unknown.                                   |
   |                                   |                                                                       |
   |                                   | **Starting**: The process is being started.                           |
   |                                   |                                                                       |
   |                                   | **Stopping**: The task is being stopped.                              |
   |                                   |                                                                       |
   |                                   | **Active_normal**: The active node is running properly.               |
   |                                   |                                                                       |
   |                                   | **Standby_normal**: The standby node is running properly.             |
   |                                   |                                                                       |
   |                                   | **Raising_active**: The node is being promoted to be the active node. |
   |                                   |                                                                       |
   |                                   | **Lowing_standby**: The node is being set to be the standby node.     |
   |                                   |                                                                       |
   |                                   | **No_action**: the action does not exist.                             |
   |                                   |                                                                       |
   |                                   | **Repairing**: The disk is being repaired.                            |
   |                                   |                                                                       |
   |                                   | **NULL**: unknown                                                     |
   +-----------------------------------+-----------------------------------------------------------------------+
   | Resource HA status                | **Normal**: the status is normal.                                     |
   |                                   |                                                                       |
   |                                   | **Exception**: indicates a fault.                                     |
   |                                   |                                                                       |
   |                                   | **Non_steady**: indicates the non-steady state.                       |
   |                                   |                                                                       |
   |                                   | **Unknown**: unknown                                                  |
   |                                   |                                                                       |
   |                                   | **NULL**: unknown                                                     |
   +-----------------------------------+-----------------------------------------------------------------------+

**Recovery Guide**:

#. Log in to the active management node and run the **su - omm** command to switch to user **omm**. Run the **${CONTROLLER_HOME}/sbin/status-oms.sh** command to check the status of OMS.

#. If floatip, okerberos, and oldap are abnormal, handle the problems by referring to ALM-12002, ALM-12004, and ALM-12005 respectively.

#. If other resources are abnormal, you are advised to view the logs of the faulty modules.

   If controller resources are abnormal, view **/var/log/Bigdata/controller/controller.log** of the faulty node.

   If CEP resources are abnormal, view **/var/log/Bigdata/omm/oms/cep/cep.log** of the faulty node.

   If AOS resources are abnormal, view **/var/log/Bigdata/controller/aos/aos.log** of the faulty node.

   If feed_watchdog resources are abnormal, view **/var/log/Bigdata/watchdog/watchdog.log** of the abnormal node.

   If HTTPD resources are abnormal, view **/var/log/Bigdata/httpd/error_log** of the abnormal node.

   If FMS resources are abnormal, view **/var/log/Bigdata/omm/oms/fms/fms.log** of the abnormal node.

   If PMS resources are abnormal, view **/var/log/Bigdata/omm/oms/pms/pms.log** of the abnormal node.

   If IAM resources are abnormal, view **/var/log/Bigdata/omm/oms/iam/iam.log** of the abnormal node.

   If the GaussDB resource is abnormal, check the **/var/log/Bigdata/omm/oms/db/omm_gaussdba.log** of the abnormal node.

   If NTP resources are abnormal, view **/var/log/Bigdata/omm/oms/ha/scriptlog/ha_ntp.log** of the abnormal node.

   If Tomcat resources are abnormal, view **/var/log/Bigdata/tomcat/catalina.log** of the abnormal node.

#. If the fault cannot be rectified based on the logs, contact O&M personnel and send the collected fault logs.

OMA Running Status
------------------

**Indicator**: OMA Running Status

**Description**: This indicator is used to check the running status of the OMA. The status can be **Running** or **Stopped**. If the OMA is **Stopped**, the OMA is unhealthy.

**Recovery Guide**:

#. Log in to the unhealthy node and run the **su - omm** command to switch to user **omm**.

#. Run **${OMA_PATH}/restart_oma_app** to manually start the OMA and check again. If the check result is still unhealthy, go to :ref:`3 <mrs_01_0294__en-us_topic_0035251772_li62867080113130>`.

#. .. _mrs_01_0294__en-us_topic_0035251772_li62867080113130:

   If manually starting the OMA cannot resolve the problem, you are advised to check the OMA logs in **/var/log/Bigdata/omm/oma/omm_agent.log**.

#. If the fault cannot be rectified based on the logs, contact O&M personnel and send the collected fault logs.

SSH Trust Between Each Node and the Active Management Node
----------------------------------------------------------

**Indicator**: SSH Trust Between Each Node and the Active Management Node

**Description**: This indicator is used to check whether the SSH mutual trust is normal. If you can switch to another node through SSH from the active OMS node as user omm without the need of entering the password, SSH communication is normal. Otherwise, SSH communication is abnormal. In addition, if you can switch to another node through SSH from the active OMS node but fail to switch to the active OMS node from the other nodes, SSH communication is abnormal.

**Recovery Guide**:

#. If the indicator check result is abnormal, the SSH trust relationships between the nodes and the active management node are abnormal. In this case, check whether the permission of the **/home/omm** directory is **omm**. If non-omm users have the directory permission, the SSH trust relationship may be abnormal. You are advised to run **chown omm:wheel** to modify the permission and check again. If the permission on the **/home/omm** directory is normal, go to :ref:`2 <mrs_01_0294__en-us_topic_0035251772_li39886844113155>`.

#. .. _mrs_01_0294__en-us_topic_0035251772_li39886844113155:

   The SSH trust relationship exception may cause heartbeat exceptions between Controller and NodeAgent, resulting in node fault alarms. In this case, rectify the fault by referring to the handling procedure of ALM-12006.

Process Running Time
--------------------

**Indicator**: Running Time of NodeAgent, Controller, and Tomcat

**Description**: This indicator is used to check the running time of the NodeAgent, Controller, and Tomcat processes. If the time is less than half an hour (1,800s), the process may have been restarted. You are advised to check the process after half an hour. If multiple check results indicate that the process runs for less than half an hour, the process is abnormal.

**Recovery Guide**:

#. Log in to the unhealthy node and run the **su - omm** command to switch to user **omm**.

#. Run the following command to check the PID based on the process name:

   **ps -ef \| grep NodeAgent**

#. Run the following command to check the process startup time based on the PID:

   **ps -p pid -o lstart**

#. Check whether the process start time is normal. If the process restarts repeatedly, go to :ref:`5 <mrs_01_0294__en-us_topic_0035251772_li38659710113226>`.

#. .. _mrs_01_0294__en-us_topic_0035251772_li38659710113226:

   View the related logs and analyze restart causes.

   If the runtime of NodeAgent is abnormal, check **/var/log/Bigdata/nodeagent/agentlog/agent.log**.

   If the Controller running time is abnormal, check the **/var/log/Bigdata/controller/controller.log** file.

   If the Tomcat running time is abnormal, check the **/var/log/Bigdata/tomcat/web.log** file.

#. If the fault cannot be rectified based on the logs, contact O&M personnel and send the collected fault logs.

Account and Password Expiration Check
-------------------------------------

**Indicator**: Account and Password Expiration Check

**Description**: This indicator checks the two operating system users **omm** and **ommdba** of MRS. For OS users, both the account and password expiration time must be checked. If the validity period of the account or password is not greater than 15 days, the account is abnormal.

**Recovery Guide**: If the validity period of the account or password is less than or equal to 15 days, contact O&M personnel.
