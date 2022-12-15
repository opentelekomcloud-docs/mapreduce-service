:original_name: alm_12037.html

.. _alm_12037:

ALM-12037 NTP Server Is Abnormal
================================

Description
-----------

This alarm is generated when the NTP server is abnormal.

This alarm is cleared when the NTP server recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12037    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+------------------------------------------------------------------------------+
| Parameter   | Description                                                                  |
+=============+==============================================================================+
| ServiceName | Specifies the service for which the alarm is generated.                      |
+-------------+------------------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.                         |
+-------------+------------------------------------------------------------------------------+
| HostName    | Specifies the IP address of the NTP server for which the alarm is generated. |
+-------------+------------------------------------------------------------------------------+

Impact on the System
--------------------

The NTP server configured on the active OMS node is abnormal. In this case, the active OMS node cannot synchronize time with the NTP server and a time offset may be generated in the cluster.

Possible Causes
---------------

-  The NTP server network is faulty.
-  The NTP server authentication fails.
-  The time cannot be obtained from the NTP server.
-  The time obtained from the NTP server is not continuously updated.

Procedure
---------

#. Check the NTP server network.

   a. On the MRS cluster details page, click the alarm from the real-time alarm list.

   b. In the **Alarm Details** area, view the additional information to check whether the NTP server fails to be pinged.

      -  If yes, go to :ref:`1.c <alm_12037__en-us_topic_0191813878_li1632254917016>`.
      -  If no, go to :ref:`2 <alm_12037__en-us_topic_0191813878_li39341571165349>`.

   c. .. _alm_12037__en-us_topic_0191813878_li1632254917016:

      Contact the O&M personnel to check the network configuration and ensure that the network between the NTP server and the active OMS node is in normal state. Then, check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_12037__en-us_topic_0191813878_li39341571165349>`.

#. .. _alm_12037__en-us_topic_0191813878_li39341571165349:

   Check whether the NTP server authentication fails.

   a. Log in to the active management node.
   b. Run **ntpq -np** to check whether the NTP server authentication fails. If **refid** of the NTP server is **.AUTH.**, the authentication fails.

      -  If yes, go to :ref:`5 <alm_12037__en-us_topic_0191813878_li572522141314>`.
      -  If no, go to :ref:`3 <alm_12037__en-us_topic_0191813878_li1771406117437>`.

#. .. _alm_12037__en-us_topic_0191813878_li1771406117437:

   Check whether the time can be obtained from the NTP server.

   a. View the alarm additional information to check whether the time cannot be obtained from the NTP server.

      -  If yes, go to :ref:`3.b <alm_12037__en-us_topic_0191813878_li3545109317619>`.
      -  If no, go to :ref:`4 <alm_12037__en-us_topic_0191813878_li2737952217524>`.

   b. .. _alm_12037__en-us_topic_0191813878_li3545109317619:

      Contact the O&M personnel to rectify the NTP server fault. After the NTP server is in normal state, check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_12037__en-us_topic_0191813878_li2737952217524>`.

#. .. _alm_12037__en-us_topic_0191813878_li2737952217524:

   Check whether the time obtained from the NTP server fails to be updated.

   a. View the alarm additional information to check whether the time obtained from the NTP server fails to be updated.

      -  If yes, go to :ref:`4.b <alm_12037__en-us_topic_0191813878_li6014697617721>`.
      -  If no, go to :ref:`5 <alm_12037__en-us_topic_0191813878_li572522141314>`.

   b. .. _alm_12037__en-us_topic_0191813878_li6014697617721:

      Contact the provider of the NTP server to rectify the NTP server fault. After the NTP server is in normal state, check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`5 <alm_12037__en-us_topic_0191813878_li572522141314>`.

#. .. _alm_12037__en-us_topic_0191813878_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
