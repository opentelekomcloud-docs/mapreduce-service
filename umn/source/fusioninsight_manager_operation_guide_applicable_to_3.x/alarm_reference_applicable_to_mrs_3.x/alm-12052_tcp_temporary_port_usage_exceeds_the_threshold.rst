:original_name: ALM-12052.html

.. _ALM-12052:

ALM-12052 TCP Temporary Port Usage Exceeds the Threshold
========================================================

Description
-----------

The system checks the TCP temporary port usage every 30 seconds and compares the actual usage with the threshold (the default threshold is 80%). This alarm is generated when the TCP temporary port usage exceeds the threshold for several times (5 times by default) consecutively.

To change the threshold, choose **O&M > Alarm** > **Thresholds** > *Name of the desired cluster* > **Host** > **Network Status** > **TCP Ephemeral Port Usage**.

When the **Trigger Count** is 1, this alarm is cleared when the TCP temporary port usage is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the TCP temporary port usage is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12052    Major          Yes
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
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

Services on the host cannot establish external connections, and therefore they are interrupted.

Possible Causes
---------------

-  The temporary port cannot meet the current service requirements.
-  The system is abnormal.

Procedure
---------

**Expand the temporary port number range.**

#. On FusionInsight Manager, click |image1| in the row where the alarm is located in the real-time alarm list and obtain the IP address of the host for which the alarm is generated.

#. Log in to the host for which the alarm is generated as user **omm**.

#. Run the **cat /proc/sys/net/ipv4/ip_local_port_range \|cut -f 1** command to obtain the value of the start port and run the **cat /proc/sys/net/ipv4/ip_local_port_range \|cut -f 2** command to obtain the value of the end port. The total number of temporary ports is the value of the end port minus the value of the start port. If the total number of temporary ports is smaller than 28,232, the random port range of the OS is narrow. Contact the system administrator to increase the port range.

#. Run the **ss -ant 2>/dev/null \| grep -v LISTEN \| awk 'NR > 2 {print $4}'|cut -d ':' -f 2 \| awk '$1 >"**\ *Value of the start port*\ **" {print $1}' \| sort -u \| wc -l** command to calculate the number of used temporary ports.

#. The formula for calculating the usage of the temporary ports is: Usage of the temporary ports = (Number of used temporary ports/Total number of temporary ports) x 100%. Check whether the temporary port usage exceeds the threshold.

   -  If yes, go to :ref:`7 <alm-12052__li39311997145458>`.
   -  If no, go to :ref:`6 <alm-12052__li61526456151427>`.

#. .. _alm-12052__li61526456151427:

   Wait for 5 minutes, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-12052__li39311997145458>`.

**Check whether the system environment is abnormal.**

7. .. _alm-12052__li39311997145458:

   Run the following command to import the temporary file and view the frequently used ports in the **port_result.txt file**:

   **netstat -tnp\ \|sort > $BIGDATA_HOME/tmp/port_result.txt**

   .. code-block::

      netstat -tnp|sort

      Active Internet connections (w/o servers)

      Proto Recv Send LocalAddress ForeignAddress State PID/ProgramName tcp   0   0 10-120-85-154:45433  10-120-85-154:9866 CLOSE_WAIT 94237/java
      tcp   0   0 10-120-85-154:45434  10-120-85-154:9866 CLOSE_WAIT 94237/java
      tcp   0   0 10-120-85-154:45435  10-120-85-154:9866 CLOSE_WAIT 94237/java
      ...

8. Run the following command to view the processes that occupy a large number of ports:

   **ps -ef \|grep** *PID*

   .. note::

      -  PID is the processes ID queried in :ref:`7 <alm-12052__li39311997145458>`.

      -  Run the following command to collect information about all processes and check the processes that occupy a large number of ports:

         **ps -ef > $BIGDATA_HOME/tmp/ps_result.txt**

9. After obtaining the administrator's approval, clear the processes that occupy a large number of ports. Wait for 5 minutes, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-12052__li57585220151427>`.

**Collect fault information.**

10. .. _alm-12052__li57585220151427:

    On the FusionInsight Manager home page of the active cluster, choose **O&M** > **Log > Download**.

11. Select **OMS** from the **Service** and click **OK**.

12. Set **Host** to the node for which the alarm is generated and the active OMS node.

13. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact the O&M personnel and send the collected log information and files **port_result.txt** and **ps_result.txt**. Then, delete the two residual temporary files from the environment.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383880.png
.. |image2| image:: /_static/images/en-us_image_0269383881.png
