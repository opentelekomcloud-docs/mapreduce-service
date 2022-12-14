:original_name: mrs_01_1639.html

.. _mrs_01_1639:

Why Does a Client Keep Failing to Connect to a Server for a Long Time?
======================================================================

Question
--------

A HBase server is faulty and cannot provide services. In this case, when a table operation is performed on the HBase client, why is the operation suspended and no response is received for a long time?

Answer
------

**Problem Analysis**

When the HBase server malfunctions, the table operation request from the HBase client is tried for several times and times out. The default timeout value is **Integer.MAX_VALUE (2147483647 ms)**. The table operation request is retired constantly during such a long period of time and is suspended at last.

**Solution**

The HBase client provides two configuration items to configure the retry and timeout of the client. :ref:`Table 1 <mrs_01_1639__te9ce661d0c4a4745b801616b66b97321>` describes them.

Set the following parameters in the **Client installation path/HBase/hbase/conf/hbase-site.xml** configuration file:

.. _mrs_01_1639__te9ce661d0c4a4745b801616b66b97321:

.. table:: **Table 1** Configuration parameters of retry and timeout

   +--------------------------------+-----------------------------------------------------------------------------------------------------+---------------+
   | Parameter                      | Description                                                                                         | Default Value |
   +================================+=====================================================================================================+===============+
   | hbase.client.operation.timeout | Client operation timeout period You need to manually add the information to the configuration file. | 2147483647 ms |
   +--------------------------------+-----------------------------------------------------------------------------------------------------+---------------+
   | hbase.client.retries.number    | Maximum retry times supported by all retryable operations.                                          | 35            |
   +--------------------------------+-----------------------------------------------------------------------------------------------------+---------------+

:ref:`Figure 1 <mrs_01_1639__fc7b1b6a1826d4b98bb68d1fd842512cb>` describes the working principles of retry and timeout.

.. _mrs_01_1639__fc7b1b6a1826d4b98bb68d1fd842512cb:

.. figure:: /_static/images/en-us_image_0000001296090588.jpg
   :alt: **Figure 1** Process for HBase client operation retry timeout

   **Figure 1** Process for HBase client operation retry timeout

The process indicates that a suspension occurs if the preceding parameters are not configured based on site requirements. It is recommended that a proper timeout period be set based on scenarios. If the operation takes a long time, set a long timeout period. If the operation takes a shot time, set a short timeout period. The number of retries can be set to **(hbase.client.retries.number)*60*1000(ms)**. The timeout period can be slightly greater than **hbase.client.operation.timeout**.
