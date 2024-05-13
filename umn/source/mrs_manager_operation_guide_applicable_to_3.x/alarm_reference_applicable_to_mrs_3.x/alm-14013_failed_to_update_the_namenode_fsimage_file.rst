:original_name: ALM-14013.html

.. _ALM-14013:

ALM-14013 Failed to Update the NameNode FsImage File
====================================================

Description
-----------

HDFS metadata is stored in the FsImage file of the NameNode data directory, which is specified by the **dfs.namenode.name.dir** configuration item. The standby NameNode periodically combines existing FsImage files and Editlog files stored in the JournalNode to generate a new FsImage file, and then pushes the new FsImage file to the data directory of the active NameNode. This period is specified by the **dfs.namenode.checkpoint.period** configuration item of HDFS. The default value is 3600s, namely, one hour. If the FsImage file in the data directory of the active NameNode is not updated, the HDFS metadata combination function is abnormal and requires rectification.

On the active NameNode, the system checks the FsImage file information every five minutes. This alarm is generated when no FsImage file is generated within three combination periods.

This alarm is cleared when a new FsImage file is generated and pushed to the active NameNode, which indicates that the HDFS metadata combination function can be properly used.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
14013    Major          Yes
======== ============== =====================

Parameters
----------

+-----------------+-------------------------------------------------------------+
| Name            | Meaning                                                     |
+=================+=============================================================+
| Source          | Specifies the cluster for which the alarm is generated.     |
+-----------------+-------------------------------------------------------------+
| ServiceName     | Specifies the service for which the alarm is generated.     |
+-----------------+-------------------------------------------------------------+
| RoleName        | Specifies the role for which the alarm is generated.        |
+-----------------+-------------------------------------------------------------+
| HostName        | Specifies the host for which the alarm is generated.        |
+-----------------+-------------------------------------------------------------+
| NameServiceName | Specifies the NameService for which the alarm is generated. |
+-----------------+-------------------------------------------------------------+

Impact on the System
--------------------

If the FsImage file in the data directory of the active NameNode is not updated, the HDFS metadata combination function is abnormal and requires rectification. If it is not rectified, the Editlog files increase continuously after HDFS runs for a period. In this case, HDFS restart is time-consuming because a large number of Editlog files need to be loaded. In addition, this alarm also indicates that the standby NameNode is abnormal and the NameNode high availability (HA) mechanism becomes invalid. When the active NameNode is faulty, the HDFS service becomes unavailable.

Possible Causes
---------------

-  The standby NameNode is stopped.
-  The standby NameNode instance is working incorrectly.
-  The standby NameNode fails to generate a new FsImage file.
-  Space of the data directory on the standby NameNode is insufficient.
-  The standby NameNode fails to push the FsImage file to the active NameNode.
-  Space of the data directory on the active NameNode is insufficient.

Procedure
---------

**Check whether the standby NameNode is stopped.**

#. On the MRS Manager portal, choose **O&M > Alarm > Alarms**. In the alarm list, click the alarm.

#. View **Location** and obtain the host name of the active NameNode for which the alarm is generated and name of the NameService where the active NameNode resides.

#. Choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Instance**, find the standby NameNode instance of the NameService in the instance list, and check whether its **Configuration Status** is **Synchronized**.

   -  If yes, go to :ref:`6 <alm-14013__li1445415191333>`.
   -  If no, go to :ref:`4 <alm-14013__li6145479091333>`.

#. .. _alm-14013__li6145479091333:

   Select the standby NameNode instance, choose **Start Instance**, and wait until the startup is complete.

#. Wait for a NameNode metadata combination period and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-14013__li1445415191333>`.

**Check whether the NameNode instance is working correctly.**

6. .. _alm-14013__li1445415191333:

   Check whether **Running Status** of the standby NameNode instance is **Normal**.

   -  If yes, go to :ref:`9 <alm-14013__li3200639691333>`.
   -  If no, go to :ref:`7 <alm-14013__li98451291333>`.

7. .. _alm-14013__li98451291333:

   Select the standby NameNode instance, choose **More** > **Restart Instance**, and wait until the startup is complete.

8. Wait for a NameNode metadata combination period and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`30 <alm-14013__li795604191333>`.

**Check whether** **the standby NameNode fails to generate a new FsImage file.**

9.  .. _alm-14013__li3200639691333:

    On the MRS Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Configurations** > **All** **Configurations**, and search and obtain the value of **dfs.namenode.checkpoint.period**. This value is the period of NameNode metadata combination.

10. Choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Instance** and obtain the service IP addresses of the active and standby NameNodes of the NameService for which the alarm is generated.

11. Click the **NameNode(**\ *xx*\ **,Standy)** and **Instance Configurations** to obtain the value of **dfs.namenode.name.dir**. This value is the FsImage storage directory of the standby NameNode.

12. Log in to the standby NameNode as user **root** or **omm**.

13. Go to the FsImage storage directory and check the generation time of the newest FsImage file.

    **cd** *Storage directory of the standby NameNode*\ **/current**

    **stat -c %y $(ls -t \| grep "fsimage_[0-9]*$" \| head -1)**

14. Run the **date** command to obtain the current system time.

15. Calculate the time difference between the generation time of the newest FsImage file and the current system time and check whether the time difference is greater than three times of the metadata combination period.

    -  If yes, go to :ref:`16 <alm-14013__li4970764591333>`.
    -  If no, go to :ref:`20 <alm-14013__li3432370991333>`.

16. .. _alm-14013__li4970764591333:

    The metadata combination function of the standby NameNode is faulty. Run the following command to check whether the fault is caused by insufficient storage space.

    Go to the FsImage storage directory and check the size of the newest FsImage file (in MB).

    **cd** *Storage directory of the standby NameNode*\ **/current**

    **du -m $(ls -t \| grep "fsimage_[0-9]*$" \| head -1) \| awk '{print $1}'**

17. Run the following command to check the available disk space of the standby NameNode (in MB).

    df -m ./ \| awk 'END{print $4}'

18. Compare the FsImage file size and the available disk space and determine whether another FsImage file can be stored on the disk.

    -  If yes, go to :ref:`7 <alm-14013__li98451291333>`.
    -  If no, go to :ref:`19 <alm-14013__li2030785791333>`.

19. .. _alm-14013__li2030785791333:

    Clear the redundant files on the disk where the directory resides to reserve sufficient space for metadata. After the clearance, wait for a NameNode metadata combination period and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`20 <alm-14013__li3432370991333>`.

**Check whether the standby NameNode fails to push the FsImage file to the active NameNode.**

20. .. _alm-14013__li3432370991333:

    Log in to the standby NameNode as user **root**.

21. Run the **su - omm** command to switch to user **omm**.

22. Run the following command to check whether the standby NameNode can push the file to the active NameNode.

    **tmpFile=/tmp/tmp_test_$(date +%s)**

    **echo "test" > $tmpFile**

    **scp $tmpFile** *Service IP address of the active NameNode*\ **:/tmp**

    -  If yes, go to :ref:`24 <alm-14013__li2740963991333>`.
    -  If no, go to :ref:`23 <alm-14013__li1279432791333>`.

23. .. _alm-14013__li1279432791333:

    When the standby NameNode fails to push data to the active NameNode as user **omm**, contact the system administrator to handle the fault. Wait for a NameNode metadata combination period and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`24 <alm-14013__li2740963991333>`.

**Check whether space on the data directory of the active NameNode is insufficient.**

24. .. _alm-14013__li2740963991333:

    On the MRS Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Instance**, click the active NameNode of the NameService for which the alarm is generated, and then click **Instance Configurations** to obtain the value of **dfs.namenode.name.dir**. This value is the FsImage storage directory of the active NameNode.

25. Log in to the active NameNode as user **root** or **omm**.

26. Go to the FsImage storage directory and check the size of the newest FsImage file (in MB).

    **cd** *Storage directory of the active NameNode*\ **/current**

    **du -m $(ls -t \| grep "fsimage_[0-9]*$" \| head -1) \| awk '{print $1}'**

27. Run the following command to check the available disk space of the active NameNode (in MB).

    df -m ./ \| awk 'END{print $4}'

28. Compare the FsImage file size and the available disk space and determine whether another FsImage file can be stored on the disk.

    -  If yes, go to :ref:`30 <alm-14013__li795604191333>`.
    -  If no, go to :ref:`29 <alm-14013__li1860623691333>`.

29. .. _alm-14013__li1860623691333:

    Clear the redundant files on the disk where the directory resides to reserve sufficient space for metadata. After the clearance, wait for a NameNode metadata combination period and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`30 <alm-14013__li795604191333>`.

**Collect fault information.**

30. .. _alm-14013__li795604191333:

    On the MRS Manager portal, choose **O&M** > **Log > Download**.

31. Select **NameNode** in the required cluster from the **Service**.

32. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

33. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927789.png
