:original_name: ALM-38011.html

.. _ALM-38011:

ALM-38011 User Connection Usage on Broker Exceeds the Threshold
===============================================================

Description
-----------

The system checks the number of connections of each user on Broker every 30 seconds. This alarm is generated when the connection usage of a user on the Broker exceeds the threshold (80% by default) for 5 consecutive times.

The number of times that smoothing is performed is **5**. This alarm is cleared when the connection usage of a user on the Broker is less than the threshold.

The alarm can be automatically cleared. However, if the number of connections of a user suddenly becomes **0** and no connection is created, the alarm cannot be automatically cleared. You need to manually clear it.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
38011    Major          Yes
======== ============== =====================

Parameters
----------

=========== ========================================================
Name        Meaning
=========== ========================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
UserName    Specifies the username for which the alarm is generated.
=========== ========================================================

Impact on the System
--------------------

If the number of connections of a user is excessive, the user cannot create new connections to the Broker.

Possible Causes
---------------

-  The number of connections (created by a user) used by the client exceeds the preset threshold.
-  The threshold for the connection usage does not meet service requirements.

Procedure
---------

**Check the number of connections established by the same user on the client.**

#. On the FusionInsight Manager home page, choose **O&M** > **Alarm** > **Alarms** > **User Connection Usage on Broker Exceeds the Threshold**. Check the host name and username of the Broker instance for which the alarm is generated in **Location**.

#. .. _alm-38011__li19192924516:

   On FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Instance**. Click the instance for which the alarm is generated to go to the page for the instance. Click the drop-down list in the upper right corner of the chart area, choose **Customize > Other**, and select **User Connection Usage on Broker**, **Maximum Number of User Connections on Broker**, and **Number of User Connections on Broker** to view the number of the current user connections on the Broker.

#. Observe the number of real-time connections of the current alarm user and check whether the real-time monitoring data of the current user exists.

   -  If yes, go to :ref:`4 <alm-38011__li7238347142216>`.
   -  If no, the current user has disconnected all connections. You need to clear the alarm manually, and no further action is required.

      .. note::

         After the alarm user disconnects all connections, the monitoring data of the user disappears. In this case, the alarm will not be automatically cleared. You need to manually clear it.

#. .. _alm-38011__li7238347142216:

   Check whether the user is authorized by the service side.

   If yes, go to :ref:`7 <alm-38011__li767116237265>`.

   If no, go to :ref:`5 <alm-38011__li10246106955>`.

#. .. _alm-38011__li10246106955:

   Run the following command on the client to limit the number of connections of the user. There are two configuration rules based on the following commands:

   a. For the specific Broker and user, run the following command:

      **kafka-configs.sh --bootstrap-server** *<broker ip:port>* **--alter --add-config 'max.connections.per.user.overrides=[**\ *<username>*\ **:**\ *<connection.number>*\ **]' --entity-type brokers --entity-name** *<broker.id>* **--command-config Kafka/kafka/config/producer.properties**

      .. note::

         For unauthorized users, confirm with the service side to reduce the maximum number of connections of an unauthorized user or set the maximum number of connections to **0**.

         In the command, you need to specify the IP address and port number of Broker, set values of configuration items, and specify the **brokerId** and **username**. Here, the user refers to the authorized Kerberos user.

         The configuration updated using the command line tool can take effect dynamically. The configuration becomes invalid after the service is restarted. To make the configuration take effect after the restart, choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Configurations** > **All** **Configurations**> **Broker** > **Server** on the FusionInsight Manager home page and update the configuration to **max.connections.per.user.overrides**.

   b. For the specific use and default Broker (that is, all Broker instances in the cluster), run the following command:

      **kafka-configs.sh --bootstrap-server** *<broker ip:port>* **--alter --add-config 'max.connections.per.user.overrides=[**\ *<username>*\ **:**\ *<connection.number>*\ **]' --entity-type brokers ---entity-default --command-config Kafka/kafka/config/client.properties**

      Example:

      **kafka-configs.sh --bootstrap-server 10.153.3.26:21007 --alter --add-config 'max.connections.per.user.overrides=[showcase:4]' --entity-type brokers --entity-name 1 --command-config Kafka/kafka/config/client.properties**

#. Check whether the maximum number of connections is **0** and whether the number of connections of the current user decreases or remains unchanged according to :ref:`2 <alm-38011__li19192924516>`.

   -  If yes, manually clear the alarm and no further action is required.
   -  If no, go to :ref:`7 <alm-38011__li767116237265>`.

#. .. _alm-38011__li767116237265:

   Check whether the number of real-time connections and connection usage of the current user are sharply increased when they are compared with historical data, and whether have exceeded the specified maximum number of connections.

   -  If yes, go to :ref:`8 <alm-38011__li73329221446>`.
   -  If no, go to :ref:`9 <alm-38011__li153332221440>`.

   .. note::

      If there is an obvious increase after the comparison and the maximum number of connections has reached the preset value, the connections of the user may be abnormal. You need to confirm with the service party.

**Check whether the number of user connections meets service requirements.**

8.  .. _alm-38011__li73329221446:

    Check whether the number of connections of the user meets service requirements.

    -  If yes, go to :ref:`9 <alm-38011__li153332221440>`.
    -  If no, contact the service party to rectify the fault.

    .. note::

       If the number of user connections is abnormal, contact the service party to rectify the fault from the following aspects:

       -  Check whether new services are added so that the number of user connections increases sharply.
       -  Check whether handle leakage occurs on the code at the service side.

9.  .. _alm-38011__li153332221440:

    Consider whether to increase the maximum number of connections of the user.

    -  If yes, go to :ref:`10 <alm-38011__li123335223414>`.
    -  If no, go to :ref:`12 <alm-38011__li17333142212420>`.

10. .. _alm-38011__li123335223414:

    Increase the maximum number of connections based on the service requirements. Set the number of connections of the user on the Kafka client. For details, see :ref:`5 <alm-38011__li10246106955>`.

11. Wait for several minutes and then check whether the alarm is automatically cleared.

    -  If yes, go to :ref:`12 <alm-38011__li17333142212420>`.
    -  If no, go to :ref:`2 <alm-38011__li19192924516>`.

12. .. _alm-38011__li17333142212420:

    Determine whether to add the user to the whitelist based on service requirements on the service side.

    -  If yes, go to :ref:`13 <alm-38011__li173338226416>`.
    -  If no, go to :ref:`15 <alm-38011__li1473912318017>`.

    .. note::

       To add a user to the whitelist, you need to restart the Kafka service. However, this operation will cause service interruption and affect service running. Therefore, you must confirm with the service side before performing this operation.

13. .. _alm-38011__li173338226416:

    On the FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Configurations** > **All Configurations** > **Broker(Role)** > **Server** to add the user to the **max.connections.per.user.whitelist** configuration item.

14. Restart the service for the modification to take effect. In addition, you need to manually clear the alarm, and no further action is required.

**Collect the fault information.**

15. .. _alm-38011__li1473912318017:

    On the FusionInsight Manager homepage, choose **O&M** > **Log** > **Download**.

16. Expand the **Service** drop-down list, and select **Kafka** for the target cluster.

17. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

18. Contact the O&M personnel and send the collected fault logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583127485.png
