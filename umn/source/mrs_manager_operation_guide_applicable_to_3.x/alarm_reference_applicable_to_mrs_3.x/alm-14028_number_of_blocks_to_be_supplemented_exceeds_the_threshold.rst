:original_name: ALM-14028.html

.. _ALM-14028:

ALM-14028 Number of Blocks to Be Supplemented Exceeds the Threshold
===================================================================

Description
-----------

The system checks the number of blocks to be supplemented every 30 seconds and compares the number with the threshold. The number of blocks to be supplemented has a default threshold. This alarm is generated when the number of blocks to be supplemented exceeds the threshold.

You can change the threshold specified by **Blocks Under Replicated (NameNode)** by choosing **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **HDFS** > **File and Block**.

If **Trigger Count** is set to **1** and the number of blocks to be supplemented is less than or equal to the threshold, this alarm is cleared. If **Trigger Count** is greater than **1** and the number of blocks to be supplemented is less than or equal to 90% of the threshold, this alarm is cleared.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14028    Minor          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------+
| Name              | Meaning                                                     |
+===================+=============================================================+
| Source            | Specifies the cluster for which the alarm is generated.     |
+-------------------+-------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.     |
+-------------------+-------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.        |
+-------------------+-------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.        |
+-------------------+-------------------------------------------------------------+
| NameServiceName   | Specifies the NameService for which the alarm is generated. |
+-------------------+-------------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.           |
+-------------------+-------------------------------------------------------------+

Impact on the System
--------------------

Data stored in HDFS is lost. HDFS may enter the security mode and cannot provide write services. Lost block data cannot be restored.

Possible Causes
---------------

-  The DataNode instance is abnormal.
-  Data is deleted.
-  The number of replicas written into the file is greater than the number of DataNodes.

Procedure
---------

#. On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. On the page that is displayed, check whether alarm **ALM-14003 Number of Lost HDFS Blocks Exceeds the Threshold** is generated.

   -  If yes, go to :ref:`2 <alm-14028__li23401293163156>`.
   -  If no, go to :ref:`3 <alm-14028__li2696171714538>`.

#. .. _alm-14028__li23401293163156:

   Rectify the fault according to the handling procedure of **ALM-14003 Number of Lost HDFS Blocks Exceeds the Threshold**. Five minutes later, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-14028__li2696171714538>`.

3. .. _alm-14028__li2696171714538:

   Log in to the HDFS client as user **root**. The user password is defined by the user before the installation. Contact the MRS cluster administrator to obtain the password. Run the following commands:

   -  Security mode:

      **cd** *Client installation directory*

      **source bigdata_env**

      **kinit hdfs**

   -  Normal mode:

      **su - omm**

      **cd** *Client installation directory*

      **source bigdata_env**

4. Run the **hdfs fsck / >> fsck.log** command to obtain the status of the current cluster.

5. Run the following command to count the number (*M*) of blocks to be replicated:

   **cat fsck.log \| grep "Under-replicated"**

6. Run the following command to count the number (*N*) of blocks to be replicated in the **/tmp/hadoop-yarn/staging/** directory:

   **cat fsck.log \| grep "Under replicated" \| grep "/tmp/hadoop-yarn/staging/" \| wc -l**

   .. note::

      **/tmp/hadoop-yarn/staging/** is the default directory. If the directory is modified, obtain it from the configuration item **yarn.app.mapreduce.am.staging-dir** in the **mapred-site.xml** file.

7. Check whether the percentage of *N* is greater than 50% (N/M > 50%).

   -  If yes, go to :ref:`8 <alm-14028__li181311850105810>`.
   -  If no, go to :ref:`9 <alm-14028__li1649292775015>`.

8. .. _alm-14028__li181311850105810:

   Run the following command to reconfigure the number of file replicas in the directory (set the number of file replicas to the number of DataNodes or the default number of file replicas):

   **hdfs dfs -setrep -w** **Number of file replicas**\ **/tmp/hadoop-yarn/staging/**

   .. note::

      To obtain the default number of file replicas:

      Log in to MRS Manager, choose **Cluster > Services > HDFS > Configurations > All Configurations**, and search for the **dfs.replication** parameter. The value of this parameter is the default number of file replicas.

   Check whether the alarm is cleared 5 minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-14028__li1649292775015>`.

**Collect the fault information.**

9.  .. _alm-14028__li1649292775015:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

10. Expand the drop-down list next to the **Service** field. In the **Services** dialog box that is displayed, select **HDFS** for the target cluster.

11. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532448206.png
