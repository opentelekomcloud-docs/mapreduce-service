:original_name: alm_24003.html

.. _alm_24003:

ALM-24003 Flume Client Connection Failure
=========================================

Description
-----------

The alarm module monitors the port connection status on the Flume server. This alarm is generated if the Flume server fails to receive a connection message from the Flume client in 3 consecutive minutes.

This alarm is cleared after the Flume server receives a connection message from the Flume client.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
24003    Major          Yes
======== ============== ==========

Parameters
----------

========== =============================================
Parameter  Description
========== =============================================
ClientIP   Specifies the IP address of the Flume client.
ServerIP   Specifies the IP address of the Flume server.
ServerPort Specifies the port on the Flume server.
========== =============================================

Impact on the System
--------------------

The communication between the Flume client and server fails. The Flume client cannot send data to the Flume server.

Possible Causes
---------------

-  The network between the Flume client and server is faulty.
-  The Flume client's process is abnormal.
-  The Flume client is incorrectly configured.

Procedure
---------

#. Check the network between the Flume client and server.

   a. Log in to the host where the alarmed Flume client resides. Run the following command to switch to user **root**:

      **sudo su - root**

   b. Run the **ping** *Flume server IP address* command to check whether the network between the Flume client and server is normal.

      -  If yes, go to :ref:`2.a <alm_24003__en-us_topic_0191813877_li33911624175511>`.
      -  If no, go to :ref:`4 <alm_24003__en-us_topic_0191813877_li572522141314>`.

#. Check whether the Flume client's process is normal.

   a. .. _alm_24003__en-us_topic_0191813877_li33911624175511:

      Log in to the host where the alarmed Flume client resides. Run the following command to switch to user **root**:

      **sudo su - root**

   b. Run the **ps -ef|grep flume \|grep client** command to check whether the Flume client process exists.

      -  If yes, go to :ref:`3.a <alm_24003__en-us_topic_0191813877_li37860237175538>`.
      -  If no, go to :ref:`4 <alm_24003__en-us_topic_0191813877_li572522141314>`.

#. Check the Flume client configuration.

   a. .. _alm_24003__en-us_topic_0191813877_li37860237175538:

      Log in to the host where the alarmed Flume client resides. Run the following command to switch to user **root**:

      **sudo su - root**

   b. Run the **cd** *Flume installation directory*\ **/fusioninsight-flume-1.6.0/conf/** command to go to Flume's configuration directory.

   c. Run the **cat properties.properties** command to query the current configuration file of the Flume client.

   d. Check whether the **properties.properties** file is correctly configured according to the configuration description of the Flume agent.

      -  If yes, go to :ref:`3.e <alm_24003__en-us_topic_0191813877_li1644380175538>`.
      -  If no, go to :ref:`4 <alm_24003__en-us_topic_0191813877_li572522141314>`.

   e. .. _alm_24003__en-us_topic_0191813877_li1644380175538:

      Modify the **properties.properties** configuration file.

   f. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_24003__en-us_topic_0191813877_li572522141314>`.

#. .. _alm_24003__en-us_topic_0191813877_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Related Information
-------------------

N/A
