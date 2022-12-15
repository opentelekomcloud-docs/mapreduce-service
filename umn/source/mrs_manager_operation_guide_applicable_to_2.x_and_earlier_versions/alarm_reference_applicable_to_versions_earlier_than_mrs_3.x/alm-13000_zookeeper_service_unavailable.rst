:original_name: alm_13000.html

.. _alm_13000:

ALM-13000 ZooKeeper Service Unavailable
=======================================

Description
-----------

The system checks the ZooKeeper service status every 30 seconds. This alarm is generated when the ZooKeeper service is unavailable.

This alarm is cleared when the ZooKeeper service recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
13000    Critical       Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Parameter   Description
=========== =======================================================
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

ZooKeeper fails to provide coordination services for upper-layer components and the components depending on ZooKeeper may not run properly.

Possible Causes
---------------

-  The ZooKeeper instance is abnormal.
-  The disk capacity is insufficient.
-  The network is faulty.
-  The DNS is installed on the ZooKeeper node.

Procedure
---------

**Check the ZooKeeper service instance status.**

#. On the MRS cluster details page, choose **Components** > **ZooKeeper** > **quorumpeer**.

   .. note::

      For MRS 1.7.2 or earlier, log in to MRS Manager and choose **Services** > **ZooKeeper** > **quorumpeer**.

#. Check whether the ZooKeeper instances are normal.

   -  If yes, go to :ref:`6 <alm_13000__en-us_topic_0191813962_li40423354145525>`.
   -  If no, go to :ref:`3 <alm_13000__en-us_topic_0191813962_li43049911145525>`.

#. .. _alm_13000__en-us_topic_0191813962_li43049911145525:

   Select instances whose status is not good and choose **More** > **Restart Instance**.

#. Check whether the instance status is good after restart.

   -  If yes, go to :ref:`5 <alm_13000__en-us_topic_0191813962_li64143807145525>`.
   -  If no, go to :ref:`19 <alm_13000__en-us_topic_0191813962_li572522141314>`.

#. .. _alm_13000__en-us_topic_0191813962_li64143807145525:

   On the **Alarms** tab page, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm_13000__en-us_topic_0191813962_li40423354145525>`.

   **Check disk status.**

#. .. _alm_13000__en-us_topic_0191813962_li40423354145525:

   On the MRS cluster details page, choose **Components** > **ZooKeeper** > **quorumpeer**, and check the host information of each node housing the ZooKeeper instance.

   .. note::

      For MRS 1.7.2 or earlier, log in to MRS Manager and choose **Services** > **ZooKeeper** > **quorumpeer** to view the host information of each node housing the ZooKeeper instance.

#. On the MRS cluster details page, click the **Nodes** tab and expand a node group.

   .. note::

      For MRS 1.7.2 or earlier, log in to MRS Manager and click **Hosts**.

#. In the **Disk Usage** column, check whether the disk space of each node housing ZooKeeper instances is insufficient (disk usage exceeds 80%).

   -  If yes, go to :ref:`9 <alm_13000__en-us_topic_0191813962_li66786352145525>`.
   -  If no, go to :ref:`11 <alm_13000__en-us_topic_0191813962_li835031145525>`.

#. .. _alm_13000__en-us_topic_0191813962_li66786352145525:

   Expand the disk capacity. For details, see :ref:`ALM-12017 Insufficient Disk Capacity <alm_12017>`.

#. On the **Alarms** tab page, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`11 <alm_13000__en-us_topic_0191813962_li835031145525>`.

   **Check network communication status.**

#. .. _alm_13000__en-us_topic_0191813962_li835031145525:

   On the Linux node housing the ZooKeeper instance, run the **ping** command to check whether the host names of other nodes housing the ZooKeeper instances can be pinged successfully.

   -  If yes, go to :ref:`15 <alm_13000__en-us_topic_0191813962_li53340623145525>`.
   -  If no, go to :ref:`12 <alm_13000__en-us_topic_0191813962_li7515284145525>`.

#. .. _alm_13000__en-us_topic_0191813962_li7515284145525:

   Modify the IP addresses in **/etc/hosts** and add the mapping between host names and IP addresses.

#. Run the **ping** command again to check whether the host names of other nodes housing the ZooKeeper instances can be pinged successfully.

   -  If yes, go to :ref:`14 <alm_13000__en-us_topic_0191813962_li15395686145525>`.
   -  If no, go to :ref:`19 <alm_13000__en-us_topic_0191813962_li572522141314>`.

#. .. _alm_13000__en-us_topic_0191813962_li15395686145525:

   On the **Alarms** tab page, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`15 <alm_13000__en-us_topic_0191813962_li53340623145525>`.

   **Check the DNS.**

#. .. _alm_13000__en-us_topic_0191813962_li53340623145525:

   Check whether the DNS is installed on the node housing the ZooKeeper instance. On the Linux node housing the ZooKeeper instance, run the **cat /etc/resolv.conf** command to check whether the file is empty.

   -  If yes, go to :ref:`16 <alm_13000__en-us_topic_0191813962_li54403854145525>`.
   -  If no, go to :ref:`19 <alm_13000__en-us_topic_0191813962_li572522141314>`.

#. .. _alm_13000__en-us_topic_0191813962_li54403854145525:

   Run the **service named status** command to check whether the DNS is started.

   -  If yes, go to :ref:`17 <alm_13000__en-us_topic_0191813962_li44636076145525>`.
   -  If no, go to :ref:`19 <alm_13000__en-us_topic_0191813962_li572522141314>`.

#. .. _alm_13000__en-us_topic_0191813962_li44636076145525:

   Run the **service named stop** command to stop the DNS service. If "Shutting down name server BIND waiting for named to shut down (28s)" is displayed, the DNS service is stopped successfully. Comment out the content (if any) in **/etc/resolv.conf**.

#. On the **Alarms** tab page, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`19 <alm_13000__en-us_topic_0191813962_li572522141314>`.

#. .. _alm_13000__en-us_topic_0191813962_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
