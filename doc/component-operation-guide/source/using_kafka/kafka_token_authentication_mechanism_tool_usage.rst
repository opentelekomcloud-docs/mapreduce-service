:original_name: mrs_01_1041.html

.. _mrs_01_1041:

Kafka Token Authentication Mechanism Tool Usage
===============================================

Scenario
--------

Operations need to be performed on tokens when the token authentication mechanism is used.

This section applies to security clusters of MRS 3.\ *x* or later.

Prerequisites
-------------

-  The system administrator has understood service requirements and prepared a system user.
-  The Kafka client has been installed.

Procedure
---------

#. Log in as a client installation user to the node on which the Kafka client is installed.

#. Switch to the Kafka client installation directory, for example, **/opt/kafkaclient**.

   **cd /opt/kafkaclient**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Run the following command to perform user authentication:

   **kinit** *Component service user*

#. Run the following command to switch to the Kafka client installation directory:

   **cd Kafka/kafka/bin**

#. Use **kafka-delegation-tokens.sh** to perform operations on tokens.

   -  Generate a token for a user.

      **./kafka-delegation-tokens.sh --create --bootstrap-server <**\ *IP1:PORT, IP2:PORT,...*\ **> --max-life-time-period <**\ *Long: max life period in milliseconds*\ **> --command-config <**\ *config file*\ **> --renewer-principal User:<**\ *user name*\ **>**

      Example: **./kafka-delegation-tokens.sh --create --bootstrap-server 192.168.1.1:21007,192.168.1.2:21007,192.168.1.3:21007 --command-config ../config/producer.properties --max-life-time-period -1 --renewer-principal User:username**

   -  List information about all tokens of a specified user.

      **./kafka-delegation-tokens.sh --describe --bootstrap-server <**\ *IP1:PORT, IP2:PORT,...*\ **> --command-config <**\ *config file*\ **> --owner-principal User:<**\ *user name*\ **>**

      Example: **./kafka-delegation-tokens.sh --describe --bootstrap-server 192.168.1.1:21007,192.168.1.2:21007,192.168.1.3:21007 --command-config ../config/producer.properties --owner-principal User:username**

   -  Update the token validity period.

      **./kafka-delegation-tokens.sh --renew --bootstrap-server <**\ *IP1:PORT, IP2:PORT,...*\ **> --renew-time-period <**\ *Long: renew time period in milliseconds*\ **> --command-config <**\ *config file*\ **> --hmac <**\ *String: HMAC of the delegation token*\ **>**

      Example: **./kafka-delegation-tokens.sh --renew --bootstrap-server 192.168.1.1:21007,192.168.1.2:21007,192.168.1.3:21007 --renew-time-period -1 --command-config ../config/producer.properties --hmac ABCDEFG**

   -  Destroy a token.

      **./kafka-delegation-tokens.sh --expire --bootstrap-server <**\ *IP1:PORT, IP2:PORT,...*\ **> --expiry-time-period <**\ *Long: expiry time period in milliseconds*\ **> --command-config <**\ *config file*\ **> --hmac <**\ *String: HMAC of the delegation token*\ **>**

      Example: **./kafka-delegation-tokens.sh --expire --bootstrap-server 192.168.1.1:21007,192.168.1.2:21007,192.168.1.3:21007 --expiry-time-period -1 --command-config ../config/producer.properties --hmac ABCDEFG**
