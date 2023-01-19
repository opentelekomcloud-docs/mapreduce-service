:original_name: mrs_01_24139.html

.. _mrs_01_24139:

Viewing Brokers on Kafka UI
===========================

Scenario
--------

On Kafka UI, you can view broker details and JMX metrics of the broker node data traffic.

Viewing a Broker
----------------

#. Log in to Kafka UI. For details, see :ref:`Accessing Kafka UI <mrs_01_24134>`.

#. Click **Brokers**. The broker details page is displayed.

#. In the **Broker Summary** area, you can view **Broker ID**, **Host**, **Rack**, **Disk(Used|Total)**, and **Memory(Used|Total)** of brokers.

   |image1|

#. In the **Brokers Metrics** area, you can view the JMX metrics of the broker node data traffic, including the average number of incoming messages per second, number of bytes of incoming messages per second, number of bytes of outgoing messages per second, and number of failed requests per second, total number of requests per second, and number of production requests per second in different time windows.

   |image2|

Searching for a Broker
----------------------

#. Log in to Kafka UI. For details, see :ref:`Accessing Kafka UI <mrs_01_24134>`.
#. Click **Brokers**. The broker details page is displayed.
#. In the upper right corner of the page, you can enter a host IP address or rack configuration information to search for a broker.

.. |image1| image:: /_static/images/en-us_image_0000001348739889.png
.. |image2| image:: /_static/images/en-us_image_0000001296219496.png
