:original_name: alm_12017.html

.. _alm_12017:

ALM-12017 Insufficient Disk Capacity
====================================

Description
-----------

The system checks the host disk usage every 30 seconds and compares the actual disk usage with the threshold. The disk usage has a default threshold. This alarm is generated if the disk usage exceeds the threshold.

To change the threshold, choose **System** > **Threshold Configuration**.

This alarm is cleared when the host disk usage is less than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12017    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------------------------------+
| Parameter         | Description                                                                         |
+===================+=====================================================================================+
| ServiceName       | Specifies the service for which the alarm is generated.                             |
+-------------------+-------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| PartitionName     | Specifies the disk partition for which the alarm is generated.                      |
+-------------------+-------------------------------------------------------------------------------------+
| Trigger Condition | Generates an alarm when the actual indicator value exceeds the specified threshold. |
+-------------------+-------------------------------------------------------------------------------------+

Impact on the System
--------------------

Service processes become unavailable.

Possible Causes
---------------

The disk configuration cannot meet service requirements. The disk usage reaches the upper limit.

Procedure
---------

#. Log in to MRS Manager and check whether the threshold is appropriate.

   a. The default threshold is 90%. You can change the threshold to meet service requirements.

      -  If yes, go to :ref:`2 <alm_12017__en-us_topic_0191813938_li1589085510271>`.
      -  If no, go to :ref:`1.b <alm_12017__en-us_topic_0191813938_li39303074103210>`.

   b. .. _alm_12017__en-us_topic_0191813938_li39303074103210:

      Choose **System** > **Threshold Configuration** and change the alarm threshold based on the actual disk usage.

   c. Wait 2 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_12017__en-us_topic_0191813938_li1589085510271>`.

#. .. _alm_12017__en-us_topic_0191813938_li1589085510271:

   Check whether the disk is a system disk.

   a. .. _alm_12017__en-us_topic_0191813938_li4203435103158:

      Go to the MRS cluster details page. In the alarm list on the alarm management tab page, click the row that contains the alarm. In the alarm details, view the host name and disk partition information.

   b. Log in to the node for which the alarm is generated.

   c. Run the **df -h** command to check the system disk partition usage. Check whether the disk is mounted to any of the following directories by using the disk partition name obtained in :ref:`2.a <alm_12017__en-us_topic_0191813938_li4203435103158>`: **/**, **/boot**, **/home**, **/opt**, **/tmp**, **/var**, **/var/log**, **/boot**, and **/srv/BigData**.

      -  If yes, the disk is a system disk. Then go to :ref:`3.a <alm_12017__en-us_topic_0191813938_li3904890010377>`.
      -  If no, the disk is not a system disk. Then go to :ref:`2.d <alm_12017__en-us_topic_0191813938_li22825392103158>`.

   d. .. _alm_12017__en-us_topic_0191813938_li22825392103158:

      Run the **df -h** command to check the system disk partition usage. Determine the role of the disk based on the disk partition name obtained in :ref:`2.a <alm_12017__en-us_topic_0191813938_li4203435103158>`.

   e. Check whether the disk is used by HDFS or Yarn.

      -  If yes, expand the disk capacity for the Core node. Then go to :ref:`2.f <alm_12017__en-us_topic_0191813938_li23401589103652>`.
      -  If no, go to :ref:`4 <alm_12017__en-us_topic_0191813938_li572522141314>`.

   f. .. _alm_12017__en-us_topic_0191813938_li23401589103652:

      Wait 2 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_12017__en-us_topic_0191813938_li1854606410341>`.

#. .. _alm_12017__en-us_topic_0191813938_li1854606410341:

   Check whether large files are written to the disk.

   a. .. _alm_12017__en-us_topic_0191813938_li3904890010377:

      Run the **find / -xdev -size +500M -exec ls -l {} \\;** command to view files larger than 500 MB on the node. Check whether such files are written to the disk.

      -  If yes, go to :ref:`3.b <alm_12017__en-us_topic_0191813938_li65656242103715>`.
      -  If no, go to :ref:`4 <alm_12017__en-us_topic_0191813938_li572522141314>`.

   b. .. _alm_12017__en-us_topic_0191813938_li65656242103715:

      Handle the large files and check whether the alarm is cleared 2 minutes later.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_12017__en-us_topic_0191813938_li572522141314>`.

   c. Expand the disk capacity.

   d. Wait 2 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_12017__en-us_topic_0191813938_li572522141314>`.

#. .. _alm_12017__en-us_topic_0191813938_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

**Reference**
-------------

None
