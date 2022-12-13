:original_name: mrs_01_1035.html

.. _mrs_01_1035:

Safety Instructions on Using Kafka
==================================

This section applies to MRS 3.\ *x* or later.

Brief Introduction to Kafka APIs
--------------------------------

-  Producer API

   Indicates the API defined in **org.apache.kafka.clients.producer.KafkaProducer**. When **kafka-console-producer.sh** is used, the API is used by default.

-  Consumer API

   Indicates the API defined in **org.apache.kafka.clients.consumer.KafkaConsumer**. When **kafka-console-consumer.sh** is used, the API is used by default.

.. note::

   In MRS 3.\ *x* or later, Kafka no longer support old Producer or Consumer APIs.

Protocol Description for Accessing Kafka
----------------------------------------

The protocols used to access Kafka are as follows: PLAINTEXT, SSL, SASL_PLAINTEXT, and SASL_SSL.

When Kafka service is started, the listeners using the PLAINTEXT and SASL_PLAINTEXT protocols are started. You can set **ssl.mode.enable** to **true** in Kafka service configuration to start listeners using SSL and SASL_SSL protocols. The following table describes the four protocols:

+----------------+-------------------------------------------------------------+--------------+
| Protocol       | Description                                                 | Default Port |
+================+=============================================================+==============+
| PLAINTEXT      | Supports plaintext access without authentication.           | 9092         |
+----------------+-------------------------------------------------------------+--------------+
| SASL_PLAINTEXT | Supports plaintext access with Kerberos authentication.     | 21007        |
+----------------+-------------------------------------------------------------+--------------+
| SSL            | Supports SSL-encrypted access without authentication.       | 9093         |
+----------------+-------------------------------------------------------------+--------------+
| SASL_SSL       | Supports SSL-encrypted access with Kerberos authentication. | 21009        |
+----------------+-------------------------------------------------------------+--------------+

ACL Settings for a Topic
------------------------

To view and set topic permission information, run the **kafka-acls.sh** script on the Linux client. For details, see :ref:`Managing Kafka User Permissions <mrs_01_0378>`.

Use of Kafka APIs in Different Scenarios
----------------------------------------

-  Scenario 1: accessing the topic with an ACL

   +-------------+-----------------------------------------------------+----------------------------------------------------------------------------------+--------------------------------------+----------------------------------------------+
   | Used API    | User Group                                          | Client Parameter                                                                 | Server Parameter                     | Accessed Port                                |
   +=============+=====================================================+==================================================================================+======================================+==============================================+
   | API         | Users need to meet one of the following conditions: | security.inter.broker.protocol=SASL_PLAINTEXT sasl.kerberos.service.name = kafka | ``-``                                | sasl.port (The default number is 21007.)     |
   |             |                                                     |                                                                                  |                                      |                                              |
   |             | -  In the administrator group                       |                                                                                  |                                      |                                              |
   |             | -  In the **kafkaadmin** group                      |                                                                                  |                                      |                                              |
   |             | -  In the **kafkasuperuser** group                  |                                                                                  |                                      |                                              |
   |             | -  In the **kafka** group and be authorized         |                                                                                  |                                      |                                              |
   +-------------+-----------------------------------------------------+----------------------------------------------------------------------------------+--------------------------------------+----------------------------------------------+
   |             |                                                     | security.protocol=SASL_SSL sasl.kerberos.service.name = kafka                    | Set **ssl.mode.enable** to **true**. | sasl-ssl.port (The default number is 21009.) |
   +-------------+-----------------------------------------------------+----------------------------------------------------------------------------------+--------------------------------------+----------------------------------------------+

-  Scenario 2: accessing the topic without an ACL

   +-------------+-----------------------------------------------------+---------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------------+
   | Used API    | User Group                                          | Client Parameter                                                    | Server Parameter                                                                                         | Accessed Port                                |
   +=============+=====================================================+=====================================================================+==========================================================================================================+==============================================+
   | API         | Users need to meet one of the following conditions: | security.protocol=SASL_PLAINTEXT sasl.kerberos.service.name = kafka | ``-``                                                                                                    | sasl.port (The default number is 21007.)     |
   |             |                                                     |                                                                     |                                                                                                          |                                              |
   |             | -  In the administrator group                       |                                                                     |                                                                                                          |                                              |
   |             | -  In the **kafkaadmin** group                      |                                                                     |                                                                                                          |                                              |
   |             | -  In the **kafkasuperuser** group                  |                                                                     |                                                                                                          |                                              |
   +-------------+-----------------------------------------------------+---------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------------+
   |             | Users are in the **kafka** group.                   |                                                                     | Set **allow.everyone.if.no.acl.found** to **true**.                                                      | sasl.port (The default number is 21007.)     |
   |             |                                                     |                                                                     |                                                                                                          |                                              |
   |             |                                                     |                                                                     | .. note::                                                                                                |                                              |
   |             |                                                     |                                                                     |                                                                                                          |                                              |
   |             |                                                     |                                                                     |    In normal mode, the server parameter **allow.everyone.if.no.acl.found** does not need to be modified. |                                              |
   +-------------+-----------------------------------------------------+---------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------------+
   |             | Users need to meet one of the following conditions: | security.protocol=SASL_SSL sasl.kerberos.service.name = kafka       | Set **ssl.mode.enable** to **true**.                                                                     | sasl-ssl.port (The default number is 21009.) |
   |             |                                                     |                                                                     |                                                                                                          |                                              |
   |             | -  In the administrator group                       |                                                                     |                                                                                                          |                                              |
   |             | -  In the **kafkaadmin** group                      |                                                                     |                                                                                                          |                                              |
   |             | -  In the **kafkasuperuser** group                  |                                                                     |                                                                                                          |                                              |
   +-------------+-----------------------------------------------------+---------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------------+
   |             | Users are in the **kafka** group.                   |                                                                     | #. Set **allow.everyone.if.no.acl.found** to **true**.                                                   | sasl-ssl.port (The default number is 21009.) |
   |             |                                                     |                                                                     | #. Set **ssl.mode.enable** to **true**.                                                                  |                                              |
   +-------------+-----------------------------------------------------+---------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------------+
   |             | ``-``                                               | security.protocol=PLAINTEXT                                         | Set **allow.everyone.if.no.acl.found** to **true**.                                                      | port (The default number is 9092.)           |
   +-------------+-----------------------------------------------------+---------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------------+
   |             | ``-``                                               | security.protocol=SSL                                               | #. Set **allow.everyone.if.no.acl.found** to **true**.                                                   | ssl.port (The default number is 9063.)       |
   |             |                                                     |                                                                     | #. Set **ssl.mode.enable** to **true**.                                                                  |                                              |
   +-------------+-----------------------------------------------------+---------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------+----------------------------------------------+
