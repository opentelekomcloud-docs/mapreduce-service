:original_name: alm_24001.html

.. _alm_24001:

ALM-24001 Flume Agent Is Abnormal
=================================

Description
-----------

This alarm is generated if the Flume agent monitoring module detects that the Flume agent process is abnormal.

This alarm is cleared after the Flume agent process recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
24001    Minor          Yes
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

Functions of the alarmed Flume agent instance are abnormal. Data transmission tasks of the instance are suspended. In real-time data transmission, data will be lost.

Possible Causes
---------------

-  The **JAVA_HOME** directory does not exist or the Java permission is incorrect.
-  The permission of the Flume agent directory is incorrect.

Procedure
---------

#. Check the Flume agent's configuration file.

   a. Log in to the host where the faulty node resides. Run the following command to switch to user **root**:

      **sudo su - root**

   b. Run the **cd** *Flume installation directory*\ **/fusioninsight-flume-1.6.0/conf/** command to go to Flume's configuration directory.

   c. Run the **cat ENV_VARS** command. Check whether the **JAVA_HOME** directory exists and whether the Flume agent user has execute permission of Java.

      -  If yes, go to :ref:`2.a <alm_24001__en-us_topic_0191813918_li53200420164950>`.
      -  If no, go to :ref:`1.d <alm_24001__en-us_topic_0191813918_li5041523116491>`.

   d. .. _alm_24001__en-us_topic_0191813918_li5041523116491:

      Specify the correct JAVA_HOME directory and grant the Flume agent user with the execute permission of Java. Then go to :ref:`2.d <alm_24001__en-us_topic_0191813918_li22464349164950>`.

#. Check the permission of the Flume agent directory.

   a. .. _alm_24001__en-us_topic_0191813918_li53200420164950:

      Log in to the host where the faulty node resides. Run the following command to switch to user **root**:

      **sudo su - root**

   b. Run the following command to access the installation directory of the Flume agent:

      **cd** *Flume agent installation directory*

   c. Run the **ls -al \* -R** command. Check whether the owner of all files is the Flume agent user.

      -  If yes, go to :ref:`3 <alm_24001__en-us_topic_0191813918_li572522141314>`.
      -  If no, run the **chown** command and change the owner of the files to the Flume agent user. Then go to :ref:`2.d <alm_24001__en-us_topic_0191813918_li22464349164950>`.

   d. .. _alm_24001__en-us_topic_0191813918_li22464349164950:

      Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_24001__en-us_topic_0191813918_li572522141314>`.

#. .. _alm_24001__en-us_topic_0191813918_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Related Information
-------------------

N/A
