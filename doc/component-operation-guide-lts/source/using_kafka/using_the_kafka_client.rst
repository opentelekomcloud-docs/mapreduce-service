:original_name: mrs_01_1767.html

.. _mrs_01_1767:

Using the Kafka Client
======================

Scenario
--------

This section guides users to use a Kafka client in an O&M or service scenario.

Prerequisites
-------------

-  The client has been installed. For example, the installation directory is **/opt/client**.
-  Service component users are created by the administrator as required. Machine-machine users need to download the keytab file. A human-machine user must change the password upon the first login. (Not involved in normal mode)
-  After changing the domain name of a cluster, redownload the client to ensure that the **kerberos.domain.name** value in the configuration file of the client is set to the correct server domain name.

Procedure
---------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to go to the client installation directory:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Run the following command to perform user authentication (skip this step in normal mode):

   **kinit** *Component service user*

#. Run the following command to switch to the Kafka client installation directory:

   **cd Kafka/kafka/bin**

#. Run the following command to use the client tool to view and use the help information:

   -  **./kafka-console-consumer.sh**: Kafka message reading tool
   -  **./kafka-console-producer.sh**: Kafka message publishing tool
   -  **./kafka-topics.sh**: Kafka topic management tool
