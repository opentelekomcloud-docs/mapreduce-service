:original_name: ALM-14011.html

.. _ALM-14011:

ALM-14011 DataNode Data Directory Is Not Configured Properly
============================================================

Description
-----------

The DataNode parameter **dfs.datanode.data.dir** specifies DataNode data directories. This alarm is generated when a configured data directory cannot be created, a data directory uses the same disk as other critical directories in the system, or multiple directories use the same disk immediately.

This alarm is cleared when the DataNode data directory is configured properly and this DataNode for which the alarm is generated is restarted.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
14011    Major          Yes
======== ============== =====================

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

If the DataNode data directory is mounted to the root directory or a critical directory, the disk space of the root directory or critical directory will be used up after long time running and the system will be faulty.

If the DataNode data directory is not configured properly, HDFS performance will deteriorate.

Possible Causes
---------------

-  The DataNode data directory fails to be created.
-  The DataNode data directory uses the same disk with critical directories, such as **/** or **/boot**.
-  Multiple directories in the DataNode data directory use the same disk.

Procedure
---------

**Check the alarm cause and information about the DataNode for which the alarm is generated.**

#. On the FusionInsight Manager portal, choose **O&M > Alarm > Alarms**. In the alarm list, click the alarm.
#. In **HostName** of **Location**, obtain the host name of the DataNode for which the alarm is generated.

**Delete directories that do not comply with the disk plan from the DataNode data directory.**

3. Choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Instance**. In the instance list, click the DataNode instance on the node for which the alarm is generated.

4. Click **Instance Configurations** and view the value of the DataNode parameter **dfs.datanode.data.dir**.

5. Check whether all DataNode data directories are consistent with the disk plan.

   -  If yes, go to :ref:`6 <alm-14011__li2148997785657>`.
   -  If no, go to :ref:`9 <alm-14011__li6692198485657>`.

6. .. _alm-14011__li2148997785657:

   Modify the DataNode parameter **dfs.datanode.data.dir** and delete the incorrect directories.

7. Choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Instance** and restart the DataNode instance.

8. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-14011__li6692198485657>`.

9. .. _alm-14011__li6692198485657:

   Log in to the DataNode for which the alarm is generated as user **root**.

   -  If the alarm cause is "The DataNode data directory fails to be created", go to :ref:`10 <alm-14011__li6509165485657>`.
   -  If the alarm cause is "The DataNode data directory uses the same disk with critical directories, such **/** or **/boot**", go to :ref:`17 <alm-14011__li6529778285657>`.
   -  If the alarm cause is "Multiple directories in the DataNode data directory uses the same disk", go to :ref:`21 <alm-14011__li3878673085657>`.

**Check whether the DataNode data directory fails to be created.**

10. .. _alm-14011__li6509165485657:

    Run the **su - omm** command to switch to user **omm**.

11. Run the **ls** command to check whether the directories exist in the DataNode data directory.

    -  If yes, go to :ref:`26 <alm-14011__li3359588885657>`.
    -  If no, go to :ref:`12 <alm-14011__li2608161785657>`.

12. .. _alm-14011__li2608161785657:

    Run the **mkdir** *data directory* command to create the directory and check whether the directory can be successfully created.

    -  If yes, go to :ref:`24 <alm-14011__li5208654485657>`.
    -  If no, go to :ref:`13 <alm-14011__li5784631085657>`.

13. .. _alm-14011__li5784631085657:

    On the FusionInsight Manager portal, choose **O&M > Alarm > Alarms** to check whether alarm **ALM-12017 Insufficient Disk Capacity** exists.

    -  If yes, go to :ref:`14 <alm-14011__li6502054785657>`.
    -  If no, go to :ref:`15 <alm-14011__li3639665285657>`.

14. .. _alm-14011__li6502054785657:

    Adjust the disk capacity and check whether alarm **ALM-12017 Insufficient Disk Capacity** is cleared. For details, see **ALM-12017 Insufficient Disk Capacity**.

    -  If yes, go to :ref:`12 <alm-14011__li2608161785657>`.
    -  If no, go to :ref:`15 <alm-14011__li3639665285657>`.

15. .. _alm-14011__li3639665285657:

    Check whether user **omm** has the **rwx** or **x** permission of all the upper-layer directories of the directory. (For example, for **/tmp/abc/**, user **omm** has the **x** permission for directory **tmp** and the **rwx** permission for directory **abc**.)

    -  If yes, go to :ref:`24 <alm-14011__li5208654485657>`.
    -  If no, go to :ref:`16 <alm-14011__li6460099185657>`.

16. .. _alm-14011__li6460099185657:

    Run the **chmod u+rwx** *path* or **chmod u+x** *path* command as user **root** to assign the **rwx** or **x** permission of these directories to user **omm**. Then go to :ref:`12 <alm-14011__li2608161785657>`.

**Check whether the DataNode data directory use the same disk as other critical directories in the system.**

17. .. _alm-14011__li6529778285657:

    Run the **df** command to obtain the disk mounting information of each directory in the DataNode data directory.

18. Check whether the directories mounted to the disk are critical directories, such as **/** or **/boot**.

    -  If yes, go to :ref:`19 <alm-14011__li20309815202314>`.
    -  If no, go to :ref:`24 <alm-14011__li5208654485657>`.

19. .. _alm-14011__li20309815202314:

    Change the value of the DataNode parameter **dfs.datanode.data.dir** and delete the directories that use the same disk as critical directories.

20. Go to :ref:`24 <alm-14011__li5208654485657>`.

**Check whether multiple directories in the DataNode data directory use the same disk.**

21. .. _alm-14011__li3878673085657:

    Run the **df** command to obtain the disk mounting information of each directory in the DataNode data directory. Record the mounted directory in the command output.

22. Modify the DataNode node parameters **dfs.datanode.data.dir** to reserve only one directory among the directories that mounted to the same disk directory.

23. Go to :ref:`24 <alm-14011__li5208654485657>`.

**Restart the DataNode and check whether the alarm is cleared.**

24. .. _alm-14011__li5208654485657:

    On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **HDFS** > **Instance** and restart the DataNode instance

25. Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`26 <alm-14011__li3359588885657>`.

**Collect fault information.**

26. .. _alm-14011__li3359588885657:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

27. Select **HDFS** in the required cluster from the **Service**.

28. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

29. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583087537.png
