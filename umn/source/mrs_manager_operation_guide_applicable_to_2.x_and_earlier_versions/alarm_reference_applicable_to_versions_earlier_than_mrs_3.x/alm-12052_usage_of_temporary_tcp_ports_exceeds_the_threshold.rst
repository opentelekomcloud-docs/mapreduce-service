:original_name: alm_12052.html

.. _alm_12052:

ALM-12052 Usage of Temporary TCP Ports Exceeds the Threshold
============================================================

Description
-----------

The system checks the usage of temporary TCP ports every 30 seconds. This alarm is generated when the usage of temporary TCP ports exceeds the threshold (the default threshold is **80%**) for multiple times (the default value is **5**).

You can change the threshold by choosing **System** > **Threshold Configuration** > **Host** > **Network Status** > **TCP Ephemeral Port Usage** > **TCP Ephemeral Port Usage**.

If the **hit number** is **1**, this alarm is cleared when the usage of temporary TCP ports is less than or equal to the threshold. If the **hit number** is greater than **1**, this alarm is cleared when the usage of temporary TCP ports is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12052    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+---------------------------------------------------------+
| Parameter         | Description                                             |
+===================+=========================================================+
| ServiceName       | Specifies the service for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.       |
+-------------------+---------------------------------------------------------+

Impact on the System
--------------------

Services on the host fail to establish connections with the external and services are interrupted.

Possible Causes
---------------

-  The temporary ports do not meet service requirements.
-  The system is abnormal.

Procedure
---------

**Expand the range of temporary ports.**

#. Go to the MRS cluster details page and choose **Alarms**.

#. In the real-time alarm list, click the alarm. In the **Alarm Details** area, obtain the IP address of the host for which the alarm is generated.

#. Use PuTTY to log in to the host for which the alarm is generated as user **omm**.

#. Run the **cat /proc/sys/net/ipv4/ip_local_port_range \|cut -f 1** command to obtain the start port number. Run the **cat /proc/sys/net/ipv4/ip_local_port_range \|cut -f 2** command to obtain the end port number. Subtract the start port number from the end port number to obtain the total number of temporary ports. If the total number of temporary ports is less than 28,232, the random port range of the OS is too small. In this case, contact the system administrator to expand the port range.

#. Run the **ss -ant 2>/dev/null \| grep -v LISTEN \| awk 'NR > 2 {print $4}'|cut -d ':' -f 2 \| awk '$1 >"**\ *start port number*\ **" {print $1}' \| sort -u \| wc -l** command to calculate the number of used temporary ports.

#. Calculate the usage of temporary ports using the following formula: Usage of temporary ports = (Number of used temporary ports/Total number of temporary ports) x 100. Check whether the usage exceeds the threshold.

   -  If yes, go to :ref:`8 <alm_12052__en-us_topic_0191813905_en-us_topic_0087039394_li62811777151245>`.
   -  If no, go to :ref:`7 <alm_12052__en-us_topic_0191813905_en-us_topic_0087039394_li5574623151245>`.

#. .. _alm_12052__en-us_topic_0191813905_en-us_topic_0087039394_li5574623151245:

   Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm_12052__en-us_topic_0191813905_en-us_topic_0087039394_li62811777151245>`.

**Check whether the system environment is normal.**

8.  .. _alm_12052__en-us_topic_0191813905_en-us_topic_0087039394_li62811777151245:

    Run the following command to import the temporary file and view the frequently used ports in the **port_result.txt** file:

    **netstat -tnp > $BIGDATA_HOME/tmp/port_result.txt**

    .. code-block::

       netstat -tnp

       Active Internet connections (w/o servers)

       Proto Recv Send LocalAddress ForeignAddress State PID/ProgramName tcp   0   0 10-120-85-154:45433  10-120-8:25009 CLOSE_WAIT 94237/java
       tcp   0   0 10-120-85-154:45434  10-120-8:25009 CLOSE_WAIT 94237/java
       tcp   0   0 10-120-85-154:45435  10-120-8:25009 CLOSE_WAIT 94237/java
       ...

9.  Run the following command to check the processes that occupy a large number of ports:

    **ps -ef \|grep** *PID*

    .. note::

       -  *PID* indicates the process ID of the port queried in :ref:`8 <alm_12052__en-us_topic_0191813905_en-us_topic_0087039394_li62811777151245>`.

       -  Run the following command to collect information about all processes in the system and check the processes that occupy a large number of ports:

          **ps -ef > $BIGDATA_HOME/tmp/ps_result.txt**

10. Contact the system administrator to clear the processes that occupy a large number of ports. Wait 5 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm_12052__en-us_topic_0191813905_li572522141314>`.

11. .. _alm_12052__en-us_topic_0191813905_li572522141314:

    Collect fault information.

    a. On MRS Manager, choose **System** > **Export Log**.
    b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
