:original_name: ALM-12101.html

.. _ALM-12101:

ALM-12101 AZ Unhealthy
======================

Description
-----------

After the AZ DR function is enabled, the system checks the AZ health status every 5 minutes. This alarm is generated when the system detects that the AZ is subhealthy or unhealthy. This alarm is cleared when the AZ becomes healthy.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12101    Critical       Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Parameter   Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
AZName      Specifies the AZ for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

The health status of an AZ is determined by whether the health status of storage resources (HDFS), computing resources (Yarn), and key roles in the AZ exceeds the configured threshold.

An AZ is subhealthy when:

-  The computing resources (Yarn) are unhealthy, but the storage resources (HDFS) are healthy. Tasks cannot be submitted to the local AZ, but data can still be read and written in the local AZ.
-  The computing resources (Yarn) are healthy, but some storage resources (HDFS) are unhealthy. Tasks can be submitted to the local AZ, and some data can be read and written in the local AZ. This depends on the locality of data detected by Spark/Hive scheduling.

An AZ is unhealthy when:

-  The computing resources (Yarn) are healthy, but the storage resources (HDFS) are unhealthy. Although tasks can be submitted to the local AZ, data cannot be read or written in the local AZ. As a result, the tasks submitted to the local AZ are invalid.
-  The computing resources (Yarn) and storage resources (HDFS) are unhealthy. Tasks cannot be submitted to the local AZ, and data cannot be read or written in the local AZ.
-  The health status of key roles except Yarn and HDFS is lower than the configured threshold.

Possible Causes
---------------

-  The computing resources (Yarn) are unhealthy.
-  The storage resources (HDFS) are unhealthy.
-  Some storage resources (HDFS) are unhealthy.
-  Key roles except Yarn and HDFS are unhealthy.

Procedure
---------

**Disable the DR drill.**

#. On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Cross-AZ HA**. The Cross-AZ HA page is displayed.

#. In the AZ DR list, check whether **Perform DR Drill** in the **Operation** column of the AZ whose health status is **Unhealthy** is gray.

   -  If yes, go to :ref:`4 <alm-12101__li57606134528>`.
   -  If no, go to :ref:`3 <alm-12101__li1076171313521>`.

#. .. _alm-12101__li1076171313521:

   Click **Restore** in the **Operation** column of the target AZ. Wait 2 minutes and refresh the page to view the health status of the AZ. Check whether the health status is normal.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-12101__li57606134528>`.

**Collect the fault information.**

4. .. _alm-12101__li57606134528:

   Log in to the active management node as user **root**.

5. View logs of unhealthy services.

   -  HDFS log files are stored in **/var/log/Bigdata/hdfs/nn/hdfs-az-state.log**.
   -  Yarn log files are stored in **/var/log/Bigdata/yarn/rm/yarn-az-state.log**.
   -  For other services, view the service health check logs in the corresponding service log directory.

6. Contact O&M personnel and provide detailed log file information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None
