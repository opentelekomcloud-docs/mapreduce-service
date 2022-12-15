:original_name: mrs_01_1581.html

.. _mrs_01_1581:

Configuring Pipeline
====================

This section applies to MRS 3.\ *x* or later clusters.

#. Configure files.

   -  **nettyconnector.registerserver.topic.storage**: (Mandatory) Configures the path (on a third-party server) to information about IP address, port numbers, and concurrency of NettySink. For example:

      .. code-block::

         nettyconnector.registerserver.topic.storage: /flink/nettyconnector

   -  **nettyconnector.sinkserver.port.range**: (Mandatory) Configures the range of port numbers of NettySink. For example:

      .. code-block::

         nettyconnector.sinkserver.port.range: 28444-28843

   -  **nettyconnector.ssl.enabled**: Configures whether to enable SSL encryption between NettySink and NettySource. The default value is **false**. For example:

      .. code-block::

         nettyconnector.ssl.enabled: true

#. Configure security authentication.

   -  SASL authentication of ZooKeeper depends on the HA configuration in the **flink-conf.yaml** file.
   -  SSL configurations such as keystore, truststore, keystore password, truststore password, and password inherit from **flink-conf.yaml**. For details, see :ref:`Encrypted Transmission <mrs_01_1583__section270112348585>`.
