:original_name: alm_12043.html

.. _alm_12043:

ALM-12043 DNS Parsing Duration Exceeds the Threshold
====================================================

Description
-----------

The system checks the DNS parsing duration every 30 seconds. This alarm is generated when the DNS parsing duration exceeds the threshold (the default threshold is 20,000 ms) for multiple times (the default value is **2**).

You can change the threshold by choosing **System** > **Threshold Configuration** > **Device** > **Host** > **Network Status** > **DNS Resolution Duration** > **DNS Resolution Duration**.

This alarm is cleared when **hit number** is **1** and the DNS resolution duration is less than or equal to the threshold. This alarm is cleared when **hit number** is not **1** and the DNS resolution duration is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12043    Major          Yes
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

-  Kerberos-based secondary authentication is slow.
-  The ZooKeeper service is abnormal.
-  The node is faulty.

Possible Causes
---------------

-  The node is configured with the DNS client.
-  The node is equipped with the DNS server and the DNS server is started.

Procedure
---------

**Check whether the node is configured with the DNS client.**

#. Go to the MRS cluster details page and choose **Alarms**.

#. View the alarm details to obtain the value of the **HostName** field in **Location**.

#. Use PuTTY to log in to the node for which the alarm is generated as user **root**.

#. Run the **cat /etc/resolv.conf** command to check whether the DNS client is installed.

   If information similar to the following is displayed, the DNS client is installed and started:

   .. code-block::

      namesever 10.2.3.4
      namesever 10.2.3.4

   -  If yes, go to :ref:`5 <alm_12043__en-us_topic_0191813958_en-us_topic_0087039385_li29935381112614>`.
   -  If no, go to :ref:`7 <alm_12043__en-us_topic_0191813958_en-us_topic_0087039385_li39250560112614>`.

#. .. _alm_12043__en-us_topic_0191813958_en-us_topic_0087039385_li29935381112614:

   Run the **vi /etc/resolv.conf** command to comment out the following content using the number signs (#) and save the file:

   .. code-block::

      # namesever 10.2.3.4
      # namesever 10.2.3.4

#. Check whether this alarm is cleared after 5 minutes.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm_12043__en-us_topic_0191813958_en-us_topic_0087039385_li39250560112614>`.

**Check whether the node is equipped with the DNS server and the DNS server is started.**

7.  .. _alm_12043__en-us_topic_0191813958_en-us_topic_0087039385_li39250560112614:

    Run the **service named status** command to check whether the DNS service is installed on the node.

    If information similar to the following is displayed, the DNS server is installed and started:

    .. code-block::

       Checking for nameserver BIND
       version: 9.6-ESV-R7-P4
       CPUs found: 8
       worker threads: 8
       number of zones: 17
       debug level: 0
       xfers running: 0
       xfers deferred: 0
       soa queries in progress: 0
       query logging is ON
       recursive clients: 4/0/1000
       tcp clients: 0/100
       server is up and running

    -  If yes, go to :ref:`8 <alm_12043__en-us_topic_0191813958_en-us_topic_0087039385_li25178791112614>`.
    -  If no, go to :ref:`10 <alm_12043__en-us_topic_0191813958_li572522141314>`.

8.  .. _alm_12043__en-us_topic_0191813958_en-us_topic_0087039385_li25178791112614:

    Run the **service named stop** command to stop the DNS server.

9.  Check whether this alarm is cleared after 5 minutes.

    -  If yes, no further action is required.
    -  If no, go to :ref:`10 <alm_12043__en-us_topic_0191813958_li572522141314>`.

10. .. _alm_12043__en-us_topic_0191813958_li572522141314:

    Collect fault information.

    a. On MRS Manager, choose **System** > **Export Log**.
    b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
