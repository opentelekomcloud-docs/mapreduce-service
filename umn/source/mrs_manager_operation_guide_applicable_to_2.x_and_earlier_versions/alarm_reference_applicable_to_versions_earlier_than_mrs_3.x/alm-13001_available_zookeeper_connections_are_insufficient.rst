:original_name: alm_13001.html

.. _alm_13001:

ALM-13001 Available ZooKeeper Connections Are Insufficient
==========================================================

Description
-----------

The system checks ZooKeeper connections every 30 seconds. This alarm is generated when the system detects that the number of used ZooKeeper instance connections exceeds the threshold (80% of the maximum connections).

This alarm is cleared when the number of used ZooKeeper instance connections is less than the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
13001    Major          Yes
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
| Trigger Condition | Generates an alarm when the actual indicator value exceeds the specified threshold. |
+-------------------+-------------------------------------------------------------------------------------+

Impact on the System
--------------------

Available ZooKeeper connections are insufficient. When the connection usage reaches 100%, external connections cannot be handled.

Possible Causes
---------------

The number of connections to the ZooKeeper node exceeds the threshold. Connection leakage occurs on some connection processes, or the maximum number of connections does not meet the requirement of the actual scenario.

Procedure
---------

#. Check the connection status.

   a. On the MRS cluster details page, choose **Alarms** > **ALM-13001 Available ZooKeeper Connections Are Insufficient** > **Location**. Check the IP address of the node for which the alarm is generated.

   b. Obtain the PID of the ZooKeeper process. Log in to the node for which this alarm is generated and run the **pgrep -f proc_zookeeper** command.

   c. Check whether the PID can be successfully obtained.

      -  If yes, go to :ref:`1.d <alm_13001__en-us_topic_0191813882_cn_58_42_000001_2_mmccppss_stepb2>`.
      -  If no, go to :ref:`2 <alm_13001__en-us_topic_0191813882_li572522141314>`.

   d. .. _alm_13001__en-us_topic_0191813882_cn_58_42_000001_2_mmccppss_stepb2:

      Obtain all the IP addresses connected to the ZooKeeper instance and the number of connections and check 10 IP addresses with top connections. Run the **lsof -i|grep $pid \| awk '{print $9}' \| cut -d : -f 2 \| cut -d \\> -f 2 \| awk '{a[$1]++} END {for(i in a){print i,a[i] \| "sort -r -g -k 2"}}' \| head -10** command based on the obtained PID value. (**$pid** is the PID obtained in the preceding step.)

   e. Check whether the node IP addresses and the number of connections are successfully obtained.

      -  If yes, go to :ref:`1.f <alm_13001__en-us_topic_0191813882_cn_58_42_000001_2_mmccppss_stepb4>`.
      -  If no, go to :ref:`2 <alm_13001__en-us_topic_0191813882_li572522141314>`.

   f. .. _alm_13001__en-us_topic_0191813882_cn_58_42_000001_2_mmccppss_stepb4:

      Obtain the ID of the port connected to the process. Run the **lsof -i|grep $pid \| awk '{print $9}'|cut -d \\> -f 2 \|grep $IP\| cut -d : -f 2** command based on the obtained PID and IP address. (**$pid** and **$IP** are the PID and IP address obtained in the preceding step.)

   g. Check whether the port ID is successfully obtained.

      -  If yes, go to :ref:`1.h <alm_13001__en-us_topic_0191813882_cn_58_42_000001_2_mmccppss_stepb5>`.
      -  If no, go to :ref:`2 <alm_13001__en-us_topic_0191813882_li572522141314>`.

   h. .. _alm_13001__en-us_topic_0191813882_cn_58_42_000001_2_mmccppss_stepb5:

      Obtain the ID of the connected process. Log in to each IP address and run the following command based on the obtained port ID: **lsof -i|grep $port**. (**$port** is the port ID obtained in the preceding step.)

   i. Check whether the process ID is successfully obtained.

      -  If yes, go to :ref:`1.j <alm_13001__en-us_topic_0191813882_stepb6>`.
      -  If no, go to :ref:`2 <alm_13001__en-us_topic_0191813882_li572522141314>`.

   j. .. _alm_13001__en-us_topic_0191813882_stepb6:

      Check whether connection leakage occurs on the process based on the obtained process ID.

      -  If yes, go to :ref:`1.k <alm_13001__en-us_topic_0191813882_stepb7>`.
      -  If no, go to :ref:`1.l <alm_13001__en-us_topic_0191813882_stepb8>`.

   k. .. _alm_13001__en-us_topic_0191813882_stepb7:

      Close the process where connection leakage occurs and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`1.l <alm_13001__en-us_topic_0191813882_stepb8>`.

   l. .. _alm_13001__en-us_topic_0191813882_stepb8:

      On the MRS cluster details page, choose **Components** > **ZooKeeper** > **Service Configuration**. Set **Type** to **All**, choose **quorumpeer** > **Performance**, and change the value of **maxCnxns** to **20000** or more.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager, choose **Services** > **ZooKeeper** > **Service Configuration**. Set **Type** to **All**, choose **quorumpeer** > **Performance**, and change the value of **maxCnxns** to **20000** or more.

   m. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_13001__en-us_topic_0191813882_li572522141314>`.

#. .. _alm_13001__en-us_topic_0191813882_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
