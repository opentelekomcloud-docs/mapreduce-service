:original_name: ALM-12089.html

.. _ALM-12089:

ALM-12089 Inter-Node Network Is Abnormal
========================================

Description
-----------

The alarm module checks the network health status of nodes in the cluster every 10 seconds. This alarm is generated when the network between two nodes is unreachable or the network status is unstable.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12089    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+-------------------------------------------------------------------+
| Name        | Meaning                                                           |
+=============+===================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated. |
+-------------+-------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.           |
+-------------+-------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

Functions of some components, such as HDFS and ZooKeeper, are affected.

Possible Causes
---------------

-  The node breaks down.
-  The network is faulty.

Procedure
---------

**Check the network health status.**

#. In the alarm list on FusionInsight Manager, click the drop-down button of the alarm and view **Additional Information**. Record the source IP address and destination IP address of the node for which the alarm is reported.

#. .. _alm-12089__li189988381537:

   Log in to the node for which the alarm is reported. On the node, ping the target node to check whether the network between the two nodes is normal.

   -  If yes, go to :ref:`6 <alm-12089__li1646022411214>`.
   -  If no, go to :ref:`3 <alm-12089__li184601124820>`.

**Check the node status.**

3. .. _alm-12089__li184601124820:

   On FusionInsight Manager, click **Host** and check whether the host list contains the faulty node to determine whether the faulty node has been removed from the cluster.

   -  If yes, go to :ref:`5 <alm-12089__li746012241226>`.
   -  If no, go to :ref:`4 <alm-12089__li19460824120>`.

4. .. _alm-12089__li19460824120:

   Check whether the faulty node is powered off.

   -  If yes, start the faulty node and go to :ref:`2 <alm-12089__li189988381537>`.
   -  If no, contact related personnel to find root cause, if need to remove the faulty nodes from the cluster and go to :ref:`5 <alm-12089__li746012241226>`, otherwise go to :ref:`6 <alm-12089__li1646022411214>`.

5. .. _alm-12089__li746012241226:

   Remove the file **$NODE_AGENT_HOME/etc/agent/hosts.ini** of all nodes in the cluster, and clean up the file **/var/log/Bigdata/unreachable/unreachable_ip_info.log**, and then manually clear the alarm.

6. .. _alm-12089__li1646022411214:

   Wait for 30 seconds and checking if the alarm was been cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-12089__li69951938132>`.

**Collect fault information.**

7.  .. _alm-12089__li69951938132:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

8.  Select **OmmAgent** from the **Service** and click **OK**.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383936.png
