:original_name: ALM-13001.html

.. _ALM-13001:

ALM-13001 Available ZooKeeper Connections Are Insufficient
==========================================================

Description
-----------

The system checks ZooKeeper connections every 60 seconds. This alarm is generated when the system detects that the number of used ZooKeeper instance connections exceeds the threshold (80% of the maximum connections).

When the **Trigger Count** is 1, this alarm is cleared when the number of used ZooKeeper instance connections is smaller than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the number of used ZooKeeper instance connections is smaller than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
13001    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service name for which the alarm is generated.                                                                 |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the host name for which the alarm is generated.                                                                    |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

Available ZooKeeper connections are insufficient. When the connection usage reaches 100%, external connections cannot be handled.

Possible Causes
---------------

The number of connections to the ZooKeeper node exceeds the threshold. Connection leakage occurs on some connection processes, or the maximum number of connections does not comply with the actual scenario.

Procedure
---------

**Check connection status.**

#. On the FusionInsight Manager portal, choose **O&M** > **Alarm** > **Alarms**. On the displayed interface, click the drop-down button of **Available ZooKeeper Connections Are Insufficient** and confirm the node IP address of the host for which the alarm is generated in the Location Information.

#. Obtain the PID of the ZooKeeper process. Log in to the node involved in this alarm as user **root** and run the **pgrep -f proc_zookeeper** command.

#. Check whether the PID can be correctly obtained.

   -  If yes, go to :ref:`4 <alm-13001__li1510096916326>`.
   -  If no, go to :ref:`15 <alm-13001__li2333852416326>`.

#. .. _alm-13001__li1510096916326:

   Obtain all the IP addresses connected to the ZooKeeper instance and the number of connections and check 10 IP addresses with top connections. Run the following command based on the obtained PID: **lsof -i|grep** *$pid* **\| awk '{print $9}' \| cut -d : -f 2 \| cut -d \\>-f 2 \| awk '{a[$1]++} END {for(i in a){print i,a[i] \| "sort -r -g -k 2"}}' \| head -10**. (The PID obtained in the preceding step is used.)

#. Check whether node IP addresses and number of connections are successfully obtained.

   -  If yes, go to :ref:`6 <alm-13001__li2774376816326>`.
   -  If no, go to :ref:`15 <alm-13001__li2333852416326>`.

#. .. _alm-13001__li2774376816326:

   Obtain the ID of the port connected to the process. Run the following command based on the obtained PID and IP address: **lsof -i|grep** *$pid* **\| awk '{print $9}'|cut -d \\> -f 2 \|grep** *$IP*\ **\| cut -d : -f 2**. (The PID and IP address obtained in the preceding step are used.)

#. Check whether the port ID is successfully obtained.

   -  If yes, go to :ref:`8 <alm-13001__li4326299016326>`.
   -  If no, go to :ref:`15 <alm-13001__li2333852416326>`.

#. .. _alm-13001__li4326299016326:

   Obtain the ID of the connected process. Log in to each IP address and run the following command based on the obtained port ID: **lsof -i|grep** *$port*. (The port ID obtained in the preceding step is used.)

#. Check whether the process ID is successfully obtained.

   -  If yes, go to :ref:`10 <alm-13001__li5163582316326>`.
   -  If no, go to :ref:`15 <alm-13001__li2333852416326>`.

#. .. _alm-13001__li5163582316326:

   Check whether connection leakage occurs on the process based on the obtained process ID.

   -  If yes, go to :ref:`11 <alm-13001__li1962513916326>`.
   -  If no, go to :ref:`12 <alm-13001__li6677995916326>`.

#. .. _alm-13001__li1962513916326:

   Close the process where connection leakage occurs and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`12 <alm-13001__li6677995916326>`.

#. .. _alm-13001__li6677995916326:

   On the FusionInsight Manager portal, choose **Cluster >** *Name of the desired cluster* **> Services** > **ZooKeeper** > **Configurations** > **All** **Configurations** > **quorumpeer** > **Performance** and increase the value of **maxCnxns** as required.

#. Save the configuration and restart the ZooKeeper service.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`15 <alm-13001__li2333852416326>`.

**Collect fault information.**

15. .. _alm-13001__li2333852416326:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

16. Select **ZooKeeper** in the required cluster from the **Service**:

17. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

18. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383942.png
