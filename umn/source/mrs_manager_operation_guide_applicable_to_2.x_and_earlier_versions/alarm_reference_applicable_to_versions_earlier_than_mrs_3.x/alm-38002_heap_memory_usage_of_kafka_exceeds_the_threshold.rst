:original_name: alm_38002.html

.. _alm_38002:

ALM-38002 Heap Memory Usage of Kafka Exceeds the Threshold
==========================================================

Description
-----------

The system checks the heap memory usage of Kafka every 30 seconds. This alarm is generated if the heap memory usage of Kafka exceeds the threshold (80%).

This alarm is cleared if the heap memory usage is lower than the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
38002    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------------------------------+
| Parameter         | Description                                                                         |
+===================+=====================================================================================+
| ServiceName       | Specifies the service for which the alarm is generated.                             |
+-------------------+-------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| Trigger Condition | Generates an alarm when the actual indicator value exceeds the specified threshold. |
+-------------------+-------------------------------------------------------------------------------------+

Impact on the System
--------------------

Memory overflow may occur, causing service crashes.

Possible Causes
---------------

The heap memory usage is high or the heap memory is improperly allocated.

Procedure
---------

#. Check the heap memory usage.

   a. Go to the MRS cluster details page and choose **Alarms**.

   b. Choose **ALM-38002 Kafka Heap Memory Usage Exceeds the Threshold** > **Location**. Query the IP address of the alarmed instance.

   c. Choose **Components > Kafka > Instance > Broker (corresponding to the IP address of the alarmed instance) > Customize > Kafka Heap Memory Resource Percentage** to check the heap memory usage.

   d. Check whether the heap memory usage of Kafka has reached the threshold (80%).

      -  If yes, go to :ref:`1.e <alm_38002__en-us_topic_0191813873_li1011493181634>`.
      -  If no, go to :ref:`2 <alm_38002__en-us_topic_0191813873_li572522141314>`.

   e. .. _alm_38002__en-us_topic_0191813873_li1011493181634:

      Choose **Components** > **Kafka** > **Service Configuration** > **All** > **Broker** > **Environment Variables**. Increase the value of **KAFKA_HEAP_OPTS** as required.

   f. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_38002__en-us_topic_0191813873_li572522141314>`.

#. .. _alm_38002__en-us_topic_0191813873_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Related Information
-------------------

N/A
