:original_name: ALM-14010.html

.. _ALM-14010:

ALM-14010 NameService Service Is Abnormal
=========================================

Description
-----------

The system checks the NameService service status every 180 seconds. This alarm is generated when the NameService service is unavailable.

This alarm is cleared when the NameService service recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14010    Major          Yes
======== ============== ==========

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

HDFS fails to provide services for upper-layer components based on the NameService service, such as HBase and MapReduce. As a result, users cannot read or write files.

Possible Causes
---------------

-  The KrbServer service is abnormal.
-  The JournalNode is faulty.
-  The DataNode is faulty.
-  The disk capacity is insufficient.
-  The NameNode enters safe mode.

Procedure
---------

**Check the KrbServer service status.**

#. On MRS Manager, choose **Cluster** > *Name of the desired cluster* > **Services**.

#. Check whether the KrbServer service exists.

   -  If yes, go to :ref:`3 <alm-14010__li4671216717852>`.
   -  If no, go to :ref:`6 <alm-14010__li2979505817852>`.

#. .. _alm-14010__li4671216717852:

   Click **KrbServer**.

#. Click **Instances**. On the KrbServer management page, select the faulty instance, and choose **More** > **Restart Instance**. Check whether the instance successfully restarts.

   -  If yes, go to :ref:`5 <alm-14010__li1076710217852>`.
   -  If no, go to :ref:`24 <alm-14010__li5097747017852>`.

#. .. _alm-14010__li1076710217852:

   Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-14010__li2979505817852>`.

**Check the JournalNode instance status.**

6.  .. _alm-14010__li2979505817852:

    On MRS Manager, choose **Cluster** > *Name of the desired cluster* > **Services**.

7.  Choose **HDFS** > **Instances**.

8.  Check whether the **Running Status** of the JournalNode is **Normal**.

    -  If yes, go to :ref:`11 <alm-14010__li1229459717852>`.
    -  If no, go to :ref:`9 <alm-14010__li34233917852>`.

9.  .. _alm-14010__li34233917852:

    Select the faulty JournalNode, and choose **More** > **Restart Instance**. Check whether the JournalNode successfully restarts.

    -  If yes, go to :ref:`10 <alm-14010__li136606617852>`.
    -  If no, go to :ref:`24 <alm-14010__li5097747017852>`.

10. .. _alm-14010__li136606617852:

    Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-14010__li1229459717852>`.

**Check the DataNode instance status.**

11. .. _alm-14010__li1229459717852:

    On MRS Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS**.

12. Click **Instances** and check whether **Running Status** of all DataNodes is **Normal**.

    -  If yes, go to :ref:`15 <alm-14010__li6155970417852>`.
    -  If no, go to :ref:`13 <alm-14010__li6039615117852>`.

13. .. _alm-14010__li6039615117852:

    Click **Instances**. On the DataNode management page, select the faulty instance, and choose **More** > **Restart Instance**. Check whether the DataNode successfully restarts.

    -  If yes, go to :ref:`14 <alm-14010__li2920958817852>`.
    -  If no, go to :ref:`15 <alm-14010__li6155970417852>`.

14. .. _alm-14010__li2920958817852:

    Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`15 <alm-14010__li6155970417852>`.

**Check disk status.**

15. .. _alm-14010__li6155970417852:

    On MRS Manager, choose **Cluster** > *Name of the desired cluster* > **Host**.

16. In the **Disk** column, check whether the disk space is insufficient.

    -  If yes, go to :ref:`17 <alm-14010__li3082265617852>`.
    -  If no, go to :ref:`19 <alm-14010__li6295063617852>`.

17. .. _alm-14010__li3082265617852:

    Expand the disk capacity.

18. Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`19 <alm-14010__li6295063617852>`.

**Check whether NameNode is in the safe mode.**

19. .. _alm-14010__li6295063617852:

    On MRS Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS**. Click **NameNode(Active)** of the abnormal NameService. The NameNode web UI is displayed.

    .. note::

       By default, the admin user does not have the management rights of other components. If the page cannot be opened or the content is not completely displayed due to insufficient permission when you access the native page of a component, you can manually create a user with the management rights of the corresponding component to log in to the component.

20. On the NameNode web UI, check whether "Safe mode is ON." is displayed.

    Information behind **Safe mode is ON** is alarm information and is displayed based actual conditions.

    -  If yes, go to :ref:`21 <alm-14010__li5459096817852>`.
    -  If no, go to :ref:`24 <alm-14010__li5097747017852>`.

21. .. _alm-14010__li5459096817852:

    Log in to the client as user **root**. Run the **cd** command to go to the client installation directory and run the **source bigdata_env** command. If the cluster uses the security mode, perform security authentication. Run the **kinit hdfs** command and enter the password as prompted. The password can be obtained from the MRS cluster administrator. If the cluster uses the non-security mode, log in as user **omm** and run the command. Ensure that user **omm** has the client execution permission.

22. Run **hdfs dfsadmin -safemode leave**.

23. Choose **O&M** > **Alarm** > **Alarms** and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`24 <alm-14010__li5097747017852>`.

**Collect the fault information.**

24. .. _alm-14010__li5097747017852:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

25. In the **Service** area, select the following nodes of the desired cluster.

    -  ZooKeeper
    -  HDFS

26. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

27. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927713.png
