:original_name: mrs_01_0282.html

.. _mrs_01_0282:

Host Health Check Indicators
============================

Swap Usage
----------

**Indicator**: Swap Usage

**Description**: Swap usage of the system. The value is calculated using the following formula: Swap usage = Used swap size/Total swap size. Assume that the current threshold is set to 75.0%. If the usage of the file handles in the system exceeds the threshold, the system is unhealthy.

**Recovery Guide**:

#. Check the swap usage of the node.

   Log in to the unhealthy node and run the **free -m** command to check the total swap space and used swap space. If the swap space usage exceeds the threshold, go to :ref:`2 <mrs_01_0282__en-us_topic_0036074522_li6576720111231>`.

#. .. _mrs_01_0282__en-us_topic_0036074522_li6576720111231:

   If the swap usage exceeds the threshold, you are advised to expand the system capacity, for example, add nodes.

Host File Handle Usage
----------------------

**Indicator**: Host File Handle Usage

**Description**: This indicator indicates the file handle usage in the system. Host file handle usage = Number of used handles/Total number of handles. If the usage exceeds the threshold, the system is unhealthy.

**Recovery Guide**:

#. Check the file handle usage of the host.

   Log in to the unhealthy node and run the **cat /proc/sys/fs/file-nr** command. In the command output, the first and third columns indicate the number of used handles and the total number of handles, respectively. If the usage exceeds the threshold, go to :ref:`2 <mrs_01_0282__en-us_topic_0036074522_li3870258111327>`.

#. .. _mrs_01_0282__en-us_topic_0036074522_li3870258111327:

   If the file handle usage of the host exceeds the threshold, you are advised to check the system and analyze the file handle usage.

NTP Offset
----------

**Indicator**: NTP Offset

**Description**: This indicator indicates the NTP time offset. If the time deviation exceeds the threshold, the system is unhealthy.

**Recovery Guide**:

#. Check the NTP time offset.

   Log in to the unhealthy node and run the **/usr/sbin/ntpq -np** command to view the information. In the command output, the **Offset** column indicates the time offset. If the time offset is greater than the threshold, go to :ref:`2 <mrs_01_0282__en-us_topic_0036074522_li4827260411417>`.

#. .. _mrs_01_0282__en-us_topic_0036074522_li4827260411417:

   If the indicator is abnormal, check whether the clock source configuration is correct. Contact O&M personnel.

Average Load
------------

**Indicator**: Average Load

**Description**: Average system load, indicating the average number of processes in the running queue in a specified period. The system average load is calculated using the load value obtained by the uptime command. Calculation method: (Load of 1 minute + Load of 5 minutes + Load of 15 minutes)/(3 x Number of CPUs). Assume that the current threshold is set to 2. If the average load exceeds 2, the system is unhealthy.

**Recovery Guide**:

#. Log in to the unhealthy node and run the **uptime** command. The last three columns in the command output indicate the load in 1 minute, 5 minutes, and 15 minutes, respectively. If the average system load exceeds the threshold, go to :ref:`2 <mrs_01_0282__en-us_topic_0036074522_li1216080711528>`.

#. .. _mrs_01_0282__en-us_topic_0036074522_li1216080711528:

   If the system average load exceeds the threshold, you are advised to perform system capacity expansion, such as adding nodes.

D State Process
---------------

**Indicator**: D State Process

**Description**: This indicator indicates the unstoppable sleep process, that is, the process in the D state. A process that is in the D state is waiting for I/O, such as disk I/O and network I/O, and experiences an I/O exception. If any process in the D state exists in the system, the system is unhealthy.

**Recovery Guide**: If the indicator is abnormal, the system generates an alarm. You are advised to handle the alarm by referring to ALM-12028.

Hardware Status
---------------

**Indicator**: Hardware Status

**Description**: This indicator is used to check the system hardware status, including the CPU, memory, disk, power supply, and fan. This indicator obtains related hardware information using **ipmitool sdr elist**. If the hardware status is abnormal, the hardware is unhealthy.

**Recovery Guide**:

#. Log in to the node where the check result is unhealthy. Run the **ipmitool sdr elist** command to check system hardware status. The last column in the command output indicates the hardware status. If the status is included in the following fault description table, the check result is unhealthy.

   +-----------------------------------+--------------------------------------------+
   | Module                            | Symptom                                    |
   +===================================+============================================+
   | Processor                         | IERR                                       |
   |                                   |                                            |
   |                                   | Thermal Trip                               |
   |                                   |                                            |
   |                                   | FRB1/BIST failure                          |
   |                                   |                                            |
   |                                   | FRB2/Hang in POST failure                  |
   |                                   |                                            |
   |                                   | FRB3/Processor startup/init failure        |
   |                                   |                                            |
   |                                   | Configuration Error                        |
   |                                   |                                            |
   |                                   | SM BIOS Uncorrectable CPU-complex Error    |
   |                                   |                                            |
   |                                   | Disabled                                   |
   |                                   |                                            |
   |                                   | Throttled                                  |
   |                                   |                                            |
   |                                   | Uncorrectable machine check exception      |
   +-----------------------------------+--------------------------------------------+
   | Power Supply                      | Failure detected                           |
   |                                   |                                            |
   |                                   | Predictive failure                         |
   |                                   |                                            |
   |                                   | Power Supply AC lost                       |
   |                                   |                                            |
   |                                   | AC lost or out-of-range                    |
   |                                   |                                            |
   |                                   | AC out-of-range, but present               |
   |                                   |                                            |
   |                                   | Config Error: Vendor Mismatch              |
   |                                   |                                            |
   |                                   | Config Error: Revision Mismatch            |
   |                                   |                                            |
   |                                   | Config Error: Processor Missing            |
   |                                   |                                            |
   |                                   | Config Error: Power Supply Rating Mismatch |
   |                                   |                                            |
   |                                   | Config Error: Voltage Rating Mismatch      |
   |                                   |                                            |
   |                                   | Config Error                               |
   +-----------------------------------+--------------------------------------------+
   | Power Unit                        | 240VA power down                           |
   |                                   |                                            |
   |                                   | Interlock power down                       |
   |                                   |                                            |
   |                                   | AC lost                                    |
   |                                   |                                            |
   |                                   | Soft-power control failure                 |
   |                                   |                                            |
   |                                   | Failure detected                           |
   |                                   |                                            |
   |                                   | Predictive failure                         |
   +-----------------------------------+--------------------------------------------+
   | Memory                            | Uncorrectable ECC                          |
   |                                   |                                            |
   |                                   | Parity                                     |
   |                                   |                                            |
   |                                   | Memory Scrub Failed                        |
   |                                   |                                            |
   |                                   | Memory Device Disabled                     |
   |                                   |                                            |
   |                                   | Correctable ECC logging limit reached      |
   |                                   |                                            |
   |                                   | Configuration Error                        |
   |                                   |                                            |
   |                                   | Throttled                                  |
   |                                   |                                            |
   |                                   | Critical Overtemperature                   |
   +-----------------------------------+--------------------------------------------+
   | Drive Slot                        | Drive Fault                                |
   |                                   |                                            |
   |                                   | Predictive Failure                         |
   |                                   |                                            |
   |                                   | Parity Check In Progress                   |
   |                                   |                                            |
   |                                   | In Critical Array                          |
   |                                   |                                            |
   |                                   | In Failed Array                            |
   |                                   |                                            |
   |                                   | Rebuild In Progress                        |
   |                                   |                                            |
   |                                   | Rebuild Aborted                            |
   +-----------------------------------+--------------------------------------------+
   | Battery                           | Low                                        |
   |                                   |                                            |
   |                                   | Failed                                     |
   +-----------------------------------+--------------------------------------------+

#. If the indicator is abnormal, contact O&M personnel.

Host Name
---------

**Indicator**: Host Name

**Description**: This indicator is used to check whether the host name is set. If the host name is not set, the system is unhealthy. If the indicator is abnormal, you are advised to set the host name properly.

**Recovery Guide**:

#. Log in to the node where the check result is unhealthy.

#. Run the hostname host name command to change the host name to ensure that the host name is consistent with the planned host name.

   **hostname**\ *host name* For example, to change the host name to **Bigdata-OM-01**, run the **hostname Bigdata-OM-01** command.

#. Modify the host name configuration file.

   Run the **vi /etc/HOSTNAME** command to edit the file. Change the file content to **Bigdata-OM-01**. Save the file, and exit.

Umask
-----

**Indicator**: Umask

**Description**: This indicator is used to check whether the umask setting of user **omm** is correct. If Umask is not 0077, the system is unhealthy.

**Recovery Guide**:

#. If the indicator is abnormal, you are advised to set umask of user **omm** to 0077. Log in to the unhealthy node and run the **su - omm** command to switch to user **omm**.
#. Run the **vi ${BIGDATA_HOME}/.om_profile** command and change the value of **umask** to **0077**. Save and exit.

OMS HA Status
-------------

**Indicator**: OMS HA Status

**Description**: This indicator is used to check whether the OMS two-node cluster resources are normal. You can run the **${CONTROLLER_HOME}/sbin/status-oms.sh** command to view the detailed information about the status of the OMS two-node cluster resources. If any module is abnormal, the OMS is unhealthy.

**Recovery Guide**:

#. Log in to the active management node and run the **su - omm** command to switch to user **omm**. Run the **${CONTROLLER_HOME}/sbin/status-oms.sh** command to check the OMS status.

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

Checking the Installation Directory and Data Directory
------------------------------------------------------

**Indicator**: Installation Directory and Data Directory Check

**Description**: This indicator checks the **lost+found** directory in the root directory of the disk partition where the installation directory (**/opt/Bigdata** by default) is located. If the directory contains the files of user **omm**, there are exceptions. When a node is abnormal, related files are stored in the **lost+found** directory. This indicator is used to check whether files are lost in such scenarios. Check the installation directory (for example, **/opt/Bigdata**) and data directory (for example, **/srv/BigData**). If any files of non-omm users exist in the two directories, the system is unhealthy.

**Recovery Guide**:

#. Log in to the unhealthy node and run the **su - omm** command to switch to user **omm**. Check whether files or folders of user omm exist in the **lost+found** directory.

   If the **omm** user file exists, you are advised to restore it and check again. If the **omm** user file does not exist, go to :ref:`2 <mrs_01_0282__en-us_topic_0036074522_li557697581195>`.

#. .. _mrs_01_0282__en-us_topic_0036074522_li557697581195:

   Check the installation directory and data directory. Check whether the files or folders of other users exist in the installation directory and data directory. If the files and folders are manually generated temporary files, you are advised to delete them and check again.

CPU Usage
---------

**Indicator**: CPU Usage

**Description**: This indicator is used to check whether the CPU usage exceeds the threshold. If the disk usage exceeds the threshold, the system is unhealthy.

**Recovery Guide**: If the indicator is abnormal, the system generates an alarm. You are advised to handle the alarm by referring to ALM-12016.

Memory Usage
------------

**Indicator**: Memory Usage

**Description**: This indicator is used to check whether the memory usage exceeds the threshold. If the disk usage exceeds the threshold, the system is unhealthy.

**Recovery Guide**: If the indicator is abnormal, the system generates an alarm. You are advised to handle the alarm by referring to ALM-12018.

Host Disk Usage
---------------

**Indicator**: Host Disk Usage

**Description**: This indicator is used to check whether the host disk usage exceeds the threshold. If the disk usage exceeds the threshold, the system is unhealthy.

**Recovery Guide**: If the indicator is abnormal, the system generates an alarm. You are advised to handle the alarm by referring to ALM-12017.

Host Disk Write Rate
--------------------

**Indicator**: Host Disk Write Rate

**Description**: This indicator is used to check the disk write rate of a host. The write rate of the host disk may vary according to the service scenario. Therefore, the value of this indicator reflects only the specified value. You need to determine whether the indicator is normal in specified service scenarios.

**Recovery Guide**: Determine whether the current disk write rate is normal based on the service scenario.

Host Disk Read Rate
-------------------

**Indicator**: Host Disk Read Rate

**Description**: This indicator is used to check the disk read rate of a host. The read rate of the host disk may vary by service scenario. Therefore, the value of this indicator reflects only the specified value. You need to determine whether the indicator is normal in specified service scenarios.

**Recovery Guide**: Determine whether the current disk read rate is normal based on the service scenario.

Host Service Plane Network Status
---------------------------------

**Indicator**: Host Service Plane Network Status

**Description**: This indicator is used to check the connectivity of the service plane network of the cluster host. If the hosts are disconnected, the cluster is unhealthy.

**Recovery Guide**: If the single-plane networking is used, check the IP address of the single plane. For a dual-plane network, the operation procedure is as follows:

#. Check the network connectivity between the service plane IP addresses of the active and standby management nodes.

   If the network is abnormal, go to :ref:`3 <mrs_01_0282__en-us_topic_0036074522_li45614056111343>`.

   If the network is normal, go to :ref:`2 <mrs_01_0282__en-us_topic_0036074522_li12524768111343>`.

#. .. _mrs_01_0282__en-us_topic_0036074522_li12524768111343:

   Check the network connectivity between the IP address of the active management node and the IP address of the abnormal node in the cluster.

#. .. _mrs_01_0282__en-us_topic_0036074522_li45614056111343:

   If the network is disconnected, contact O&M personnel to rectify the network fault to ensure that the network meets service requirements.

Host Status
-----------

**Indicator**: Host Status

**Description**: This indicator is used to check whether the host status is normal. If a node is faulty, the host is unhealthy.

**Recovery Guide**: If the indicator is abnormal, rectify the fault by referring to ALM-12006.

Alarm Check
-----------

**Indicator**: Alarm Check

**Description**: This indicator is used to check whether alarms exist on the host. If alarms exist, the service is unhealthy.

**Recovery Guide**: If this indicator is abnormal, you can rectify the fault by referring to the alarm handling guide.
