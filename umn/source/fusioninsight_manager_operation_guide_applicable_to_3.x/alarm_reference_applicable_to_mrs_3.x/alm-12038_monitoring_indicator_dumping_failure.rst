:original_name: ALM-12038.html

.. _ALM-12038:

ALM-12038 Monitoring Indicator Dumping Failure
==============================================

Description
-----------

After monitoring indicator dumping is configured on FusionInsight Manager, the system checks the monitoring indicator dumping result at the dumping interval (60 seconds by default). This alarm is generated when the dumping fails.

This alarm is cleared when dumping is successful.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12038    Major          Yes
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

The upper-layer management system cannot obtain monitoring indicators from the FusionInsight Manager system.

Possible Causes
---------------

-  The server cannot be connected.
-  The save path on the server cannot be accessed.
-  The monitoring indicator file fails to be uploaded.

Procedure
---------

**Check whether the server connection is normal.**

#. Check whether the network between the FusionInsight Manager system and the server is normal.

   -  If yes, go to :ref:`3 <alm-12038__li44378490103617>`.
   -  If no, go to :ref:`2 <alm-12038__li59131350103617>`.

#. .. _alm-12038__li59131350103617:

   Contact the network administrator to recover the network and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-12038__li44378490103617>`.

#. .. _alm-12038__li44378490103617:

   Choose **System** > **Interconnection > Upload Performance Data** and check whether the FTP username, password, port, dump mode, and public key configured on the upload performance data page are consistent with the configuration on the server.

   -  If yes, go to :ref:`5 <alm-12038__li31439394103617>`.
   -  If no, go to :ref:`4 <alm-12038__li38260071103617>`.

#. .. _alm-12038__li38260071103617:

   Enter the correct configuration information, click **OK**, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-12038__li31439394103617>`.

**Check the permission of the save path on the server is correct.**

5. .. _alm-12038__li31439394103617:

   Choose **System** > **Interconnection > Upload Performance Data** and check the configuration items **FTP Username**, **Save Path**, and **Dump Mode**.

   -  If the dump mode is FTP, go to :ref:`6 <alm-12038__li58736977103617>`.
   -  If the dump mode is SFTP, go to :ref:`7 <alm-12038__li38059143103617>`.

6. .. _alm-12038__li58736977103617:

   Log in to the server in FTP mode. In the default path, check whether **FTP Username** has the read and write permission of the relative path **Save Path**.

   -  If yes, go to :ref:`9 <alm-12038__li35446984103617>`.
   -  If no, go to :ref:`8 <alm-12038__li47558825103617>`.

7. .. _alm-12038__li38059143103617:

   Log in to the server in SFTP mode and check whether **FTP Username** has the read and write permission of the absolute path **Save Path**.

   -  If yes, go to :ref:`9 <alm-12038__li35446984103617>`.
   -  If no, go to :ref:`8 <alm-12038__li47558825103617>`.

8. .. _alm-12038__li47558825103617:

   Add the read and write permission and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-12038__li35446984103617>`.

**Check whether the save path on the server has sufficient disk space.**

9.  .. _alm-12038__li35446984103617:

    Log in to the server and check whether the save path has sufficient disk space.

    -  If yes, go to :ref:`11 <alm-12038__li51692141103617>`.
    -  If no, go to :ref:`10 <alm-12038__li53095195103617>`.

10. .. _alm-12038__li53095195103617:

    Delete unnecessary files or go to the monitoring indicator dumping configuration page to change the save path. Then, check whether the save path has sufficient disk space.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-12038__li51692141103617>`.

**Collect fault information.**

11. .. _alm-12038__li51692141103617:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

12. Select **OMS** from the **Service** and click **OK**.

13. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927442.png
