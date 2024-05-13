:original_name: admin_guide_000281.html

.. _admin_guide_000281:

Configuring Kafka Data Encryption During Transmission
=====================================================

Scenario
--------

Data between the Kafka client and the broker is transmitted in plain text. The Kafka client may be deployed in an untrusted network, exposing the transmitting data to leakage and tampering risks.

Procedure
---------

The channel between components is not encrypted by default. You can set the following parameters to enable security channel encryption.

Page access for setting parameters: On MRS Manager, click **Cluster**, click the name of the desired cluster, and choose **Services** > **Kafka**. On the displayed page, click **Configuration** and click **All Configurations**. Enter a parameter name in the search box.

.. note::

   After the configuration, restart the corresponding service for the settings to take effect.

:ref:`Table 1 <admin_guide_000281__en-us_topic_0046736711_d0e28839>` describes the parameters related to transmission encryption on the Kafka server.

.. _admin_guide_000281__en-us_topic_0046736711_d0e28839:

.. table:: **Table 1** Parameters relevant to Kafka data encryption during transmission

   +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------+
   | Parameter                      | Description                                                                                                                                                                             | Default Value  |
   +================================+=========================================================================================================================================================================================+================+
   | ssl.mode.enable                | Indicates whether to enable the Secure Sockets Layer (SSL) protocol. If this parameter is set to **true**, services relevant to the SSL protocol are started during the broker startup. | false          |
   +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------+
   | security.inter.broker.protocol | Indicates communication protocol between brokers. The communication protocol can be PLAINTEXT, SSL, SASL_PLAINTEXT, or SASL_SSL.                                                        | SASL_PLAINTEXT |
   +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------+

The SSL protocol can be configured for the server or client to encrypt transmission and communication only after **ssl.mode.enable** is set to **true** and broker enables the **SSL** and **SASL_SSL** protocols.
