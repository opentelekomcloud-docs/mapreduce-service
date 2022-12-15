:original_name: ALM-12064.html

.. _ALM-12064:

ALM-12064 Host Random Port Range Conflicts with Cluster Used Port
=================================================================

Alarm Description
-----------------

The system checks whether the random port range of the host conflicts with the range of ports used by the Cluster system every hour. The alarm is generated if they conflict. The alarm is automatically cleared when the random port range of the host is changed to the normal range.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12064    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+---------------------------------------------------------------------+
| Parameter   | Description                                                         |
+=============+=====================================================================+
| Source      | Specifiestheclusterorsystemforwhichthealarmisgenerated.             |
+-------------+---------------------------------------------------------------------+
| ServiceName | Specifies the name of the service for which the alarm is generated. |
+-------------+---------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.                |
+-------------+---------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.                |
+-------------+---------------------------------------------------------------------+

Impact on the System
--------------------

The default port of the Cluster system is occupied. As a result, some processes fail to be started.

Possible Causes
---------------

The random port range configuration is modified.

Procedure
---------

**Check the random port range of the system.**

#. In the alarm list on FusionInsight Manager, locate the row that contains the alarm, and view the IP address of the host for which the alarm is generated.

#. Log in to the host where the alarm is generated as user **root**.

#. Run the **cat /proc/sys/net/ipv4/ip_local_port_range** command to obtain the random port range of the host and check whether the minimum value is smaller than 32768.

   -  If it is, go to :ref:`4 <alm-12064__li1796713455375>`.
   -  If it is not, goto :ref:`7 <alm-12064__li1396704514377>`.

#. .. _alm-12064__li1796713455375:

   Run the **vim /etc/sysctl.conf** command to change the value of **net.ipv4.ip_local_port_range** to **32768 61000**. If this parameter does not exist, add the following configuration: **net.ipv4.ip_local_port_range = 32768 61000**.

#. Run the **sysctl -p /etc/sysctl.conf** command for the modification to take effect.

#. One hour later, check whether the alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`7 <alm-12064__li1396704514377>`.

**Collect fault information.**

7.  .. _alm-12064__li1396704514377:

    On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

8.  Select **NodeAgent** for **Service** and click **OK**.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383909.png
