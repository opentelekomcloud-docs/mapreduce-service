:original_name: alm_12038.html

.. _alm_12038:

ALM-12038 Monitoring Indicator Dump Failure
===========================================

Description
-----------

This alarm is generated when dumping fails after monitoring indicator dumping is configured on MRS Manager.

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

=========== =======================================================
Parameter   Description
=========== =======================================================
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

The upper-layer management system fails to obtain monitoring indicators from the MRS Manager system.

Possible Causes
---------------

-  The server cannot be connected.
-  The save path on the server cannot be accessed.
-  The monitoring indicator file fails to be uploaded.

Procedure
---------

#. Contact the O&M personnel to check whether the network connection between the MRS Manager system and the server is normal.

   -  If yes, go to :ref:`3 <alm_12038__en-us_topic_0191813891_li17073310143018>`.
   -  If no, go to :ref:`2 <alm_12038__en-us_topic_0191813891_li51875580143018>`.

#. .. _alm_12038__en-us_topic_0191813891_li51875580143018:

   Contact the O&M personnel to restore the network and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm_12038__en-us_topic_0191813891_li17073310143018>`.

#. .. _alm_12038__en-us_topic_0191813891_li17073310143018:

   Choose **System** > **Monitor Dumping Configuration** and check whether the FTP username, password, port, dump mode, and public key configured on the monitoring indicator dumping configuration page are consistent with those on the server.

   -  If yes, go to :ref:`5 <alm_12038__en-us_topic_0191813891_li33278826143018>`.
   -  If no, go to :ref:`4 <alm_12038__en-us_topic_0191813891_li52527297143018>`.

#. .. _alm_12038__en-us_topic_0191813891_li52527297143018:

   Enter the correct configuration, click **OK**, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm_12038__en-us_topic_0191813891_li33278826143018>`.

#. .. _alm_12038__en-us_topic_0191813891_li33278826143018:

   Choose **System** > **Monitor Dumping Configuration** and check the configuration items, including the FTP username, save path, and dumping mode.

   -  If the FTP mode is used, go to :ref:`6 <alm_12038__en-us_topic_0191813891_li8535940143050>`.
   -  If the SFTP mode is used, go to :ref:`7 <alm_12038__en-us_topic_0191813891_li35514800143050>`.

#. .. _alm_12038__en-us_topic_0191813891_li8535940143050:

   Log in to the server. In the default path, check whether the save path (relative path) has the read and write permission on the FTP username.

   -  If yes, go to :ref:`9 <alm_12038__en-us_topic_0191813891_li49122127143428>`.
   -  If no, go to :ref:`8 <alm_12038__en-us_topic_0191813891_li28538792143050>`.

#. .. _alm_12038__en-us_topic_0191813891_li35514800143050:

   Log in to the server. In the default path, check whether the save path (absolute path) has the read and write permission on the FTP username.

   -  If yes, go to :ref:`9 <alm_12038__en-us_topic_0191813891_li49122127143428>`.
   -  If no, go to :ref:`8 <alm_12038__en-us_topic_0191813891_li28538792143050>`.

#. .. _alm_12038__en-us_topic_0191813891_li28538792143050:

   Add the read and write permission and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm_12038__en-us_topic_0191813891_li49122127143428>`.

#. .. _alm_12038__en-us_topic_0191813891_li49122127143428:

   Log in to the server and check whether the save path has sufficient disk space.

   -  If yes, go to :ref:`11 <alm_12038__en-us_topic_0191813891_li572522141314>`.
   -  If no, go to :ref:`10 <alm_12038__en-us_topic_0191813891_li18335278143435>`.

#. .. _alm_12038__en-us_topic_0191813891_li18335278143435:

   Delete unnecessary files or go to the monitoring indicator dumping configuration page to change the save path. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`11 <alm_12038__en-us_topic_0191813891_li572522141314>`.

#. .. _alm_12038__en-us_topic_0191813891_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
