:original_name: ALM-12076.html

.. _ALM-12076:

ALM-12076 GaussDB Resource Is Abnormal
======================================

Description
-----------

HA checks the Manager database every 10 seconds. This alarm is generated when HA detects that the database is abnormal for 3 consecutive times.

This alarm is cleared when the database is normal.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12076    Major          Yes
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

If databases are abnormal, all core services and related service processes, such as alarms and monitoring functions, are affected.

Possible Causes
---------------

An exception occurs in the database.

Procedure
---------

**Check the database status of the active and standby management nodes.**

#. Log in to the active and standby management nodes respectively as user **root**. Run the **su - ommdba** command to switch to user **ommdba**, and then run the **gs_ctl query** command to check whether the following information is displayed in the command output.

   Command output of the active management node:

   .. code-block::

       Ha state:
              LOCAL_ROLE: Primary
              STATIC_CONNECTIONS            : 1
              DB_STATE                      : Normal
              DETAIL_INFORMATION            : user/password invalid
       Senders info:
              No information
       Receiver info:
              No information

   Command output of the standby management node:

   .. code-block::

       Ha state:
              LOCAL_ROLE: Standby
              STATIC_CONNECTIONS            : 1
              DB_STATE                      : Normal
              DETAIL_INFORMATION            : user/password invalid
       Senders info:
              No information
       Receiver info:
              No information

   -  If it is, go to :ref:`3 <alm-12076__li251973518126>`.
   -  If it is not, go to :ref:`2 <alm-12076__li1051911355122>`.

#. .. _alm-12076__li1051911355122:

   Contact the network administrator to check whether the network is faulty.

   -  If it is, go to :ref:`3 <alm-12076__li251973518126>`.
   -  If it is not, go to :ref:`5 <alm-12076__li151723519124>`.

#. .. _alm-12076__li251973518126:

   Five minutes later, check whether the alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`4 <alm-12076__li85203358122>`.

#. .. _alm-12076__li85203358122:

   Log in to the active and standby management nodes, run the **su -omm** command to switch to user **omm**, go to the **${BIGDATA_HOME} /om-server/om/sbin/** directory, and run the **status-oms.sh** script to check whether the floating IP addresses and GaussDB resources of the active and standby FusionInsight Managers are in the status shown in the following figure.

   |image1|

   -  If they are, find the alarm in the alarm list and manually clear the alarm.
   -  If they are not, go to :ref:`5 <alm-12076__li151723519124>`.

**Collect fault information.**

5. .. _alm-12076__li151723519124:

   On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

6. Select **OmmServer** for **Service** and click **OK**.

7. Click |image2| in the upper right corner. In the displayed dialog box, set **Start Date** and **End Date** to 10 minutes before and after the alarm generation time respectively and click **OK**. Then, click **Download**.

8. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

This alarm will be automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383921.jpg
.. |image2| image:: /_static/images/en-us_image_0269383922.png
