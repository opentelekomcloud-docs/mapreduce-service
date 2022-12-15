:original_name: mrs_08_0024.html

.. _mrs_08_0024:

Message Notification
====================

Feature Introduction
--------------------

The following operations are often performed during the running of a big data cluster:

-  Big data clusters often change, for example, cluster scale-out and scale-in.
-  When a service data volume changes abruptly, auto scaling will be triggered.
-  After related services are stopped, a big data cluster needs to be stopped.

To immediately notify you of successful operations, cluster unavailability, and node faults, MRS uses Simple Message Notification (SMN) to send notifications to you through SMS and emails, facilitating maintenance.

Customer Benefits
-----------------

After configuring SMN, you can receive MRS cluster health status, updates, and component alarms through SMS or emails in real time. MRS sends real-time monitoring and alarm notification to help you easily perform O&M and efficiently deploy big data services.

Feature Description
-------------------

MRS uses SMN to provide one-to-multiple message subscription and notification over a variety of protocols.

You can create a topic and configure topic policies to control publisher and subscriber permissions on the topic. MRS sends cluster messages to the topic to which you have permission to publish messages. Then, all subscribers who subscribe to the topic can receive cluster updates and component alarms through SMS and emails.


.. figure:: /_static/images/en-us_image_0000001296750222.png
   :alt: **Figure 1** Implementation process

   **Figure 1** Implementation process
