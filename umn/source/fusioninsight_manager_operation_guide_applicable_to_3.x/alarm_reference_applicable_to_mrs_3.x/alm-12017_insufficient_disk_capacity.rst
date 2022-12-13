:original_name: ALM-12017.html

.. _ALM-12017:

ALM-12017 Insufficient Disk Capacity
====================================

Description
-----------

The system checks the host disk usage of the system every 30 seconds and compares the actual disk usage with the threshold. The disk usage has a default threshold, this alarm is generated when the host disk usage exceeds the specified threshold.

When the **Trigger Count** is 1, this alarm is cleared when the usage of a host disk partition is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the usage of a host disk partition is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12017    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster or system for which the alarm is generated.                                                            |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| PartitionName     | Specifies the device partition for which the alarm is generated.                                                             |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

Service processes become unavailable.

Possible Causes
---------------

-  The alarm threshold is incorrect.
-  Disk configuration of the server cannot meet service requirements.

Procedure
---------

**Check whether the alarm threshold is appropriate.**

#. Log in to FusionInsight Manager, choose **O&M** > **Alarm >** **Thresholds** **>** *Name of the desired cluster* > **Host** > **Disk** > **Disk Usage** and check whether the threshold (configurable, 90% by default) is appropriate.

   -  If yes, go to :ref:`2 <alm-12017__li1280611085745>`.
   -  If no, go to :ref:`4 <alm-12017__li2782670585745>`.

#. .. _alm-12017__li1280611085745:

   Choose **O&M** > **Alarm >** **Thresholds** **>** *Name of the desired cluster* > **Host** > **Disk** > **Disk Usage** and click **Modify** in the **Operation** column to change the alarm threshold based on site requirements. As shown in :ref:`Figure 1 <alm-12017__fig6063892885745>`:

   .. _alm-12017__fig6063892885745:

   .. figure:: /_static/images/en-us_image_0000001440977873.png
      :alt: **Figure 1** Setting an alarm threshold

      **Figure 1** Setting an alarm threshold

#. After 2 minutes, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-12017__li2782670585745>`.

**Check whether the disk usage reaches the upper limit.**

4.  .. _alm-12017__li2782670585745:

    In the alarm list on FusionInsight Manager, click |image1| in the row where the alarm is located to view the alarm host name and disk partition information in the alarm details.

5.  Log in to the node where the alarm is generated as user **root**.

6.  Run the **df -lmPT \| awk '$2 != "iso9660"' \| grep '^/dev/' \| awk '{"readlink -m "$1 \| getline real }{$1=real; print $0}' \| sort -u -k 1,1** command to check the system disk partition usage. Check whether the disk is mounted to the following directories based on the disk partition name obtained in :ref:`4 <alm-12017__li2782670585745>`: **/**, **/opt**, **/tmp**, **/var**, **/var/log**, and **/srv/BigData**\ (can be customized).

    -  If yes, the disk is a system disk. Then go to :ref:`10 <alm-12017__li6170195385745>`.
    -  If no, the disk is not a system disk. Then go to :ref:`7 <alm-12017__li1190839985745>`.

7.  .. _alm-12017__li1190839985745:

    Run the **df -lmPT \| awk '$2 != "iso9660"' \| grep '^/dev/' \| awk '{"readlink -m "$1 \| getline real }{$1=real; print $0}' \| sort -u -k 1,1** command to check the system disk partition usage. Determine the role of the disk based on the disk partition name obtained in :ref:`4 <alm-12017__li2782670585745>`.

8.  Check the disk service.

    In MRS, check whether the disk service is HDFS, Yarn, Kafka, Supervisor.

    -  If yes, adjust the capacity. Then go to :ref:`9 <alm-12017__li1354951085745>`.
    -  If no, go to :ref:`12 <alm-12017__li1359113885745>`.

9.  .. _alm-12017__li1354951085745:

    After 2 minutes, check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-12017__li1359113885745>`.

10. .. _alm-12017__li6170195385745:

    Run the **find / -xdev -size +500M -execls -l {} \\;** command to check whether a file larger than 500 MB exists on the node and disk.

    -  If yes, go to :ref:`11 <alm-12017__li3133628885745>`.
    -  If no, go to :ref:`12 <alm-12017__li1359113885745>`.

11. .. _alm-12017__li3133628885745:

    Handle the large file and check whether the alarm is cleared 2 minutes later.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-12017__li1359113885745>`.

12. .. _alm-12017__li1359113885745:

    Contact the system administrator to expand the disk capacity.

13. After 2 minutes, check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`14 <alm-12017__li5603307085745>`.

**Collect fault information.**

14. .. _alm-12017__li5603307085745:

    On FusionInsight Manager, choose **O&M** > **Log > Download**.

15. Select **OMS** from the **Service** and click **OK**.

16. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

17. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383828.png
.. |image2| image:: /_static/images/en-us_image_0269383829.png
