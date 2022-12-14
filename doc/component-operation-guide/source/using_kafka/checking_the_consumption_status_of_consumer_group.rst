:original_name: mrs_01_1039.html

.. _mrs_01_1039:

Checking the Consumption Status of Consumer Group
=================================================

Scenario
--------

This section describes how to view the current expenditure on the client based on service requirements.

This section applies to MRS 3.\ *x* or later.

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

#. Run the following command to perform user authentication (skip this step in normal mode):

   **kinit** *Component service user*

#. Run the following command to switch to the Kafka client installation directory:

   **cd Kafka/kafka/bin**

#. Run the **kafka-consumer-groups.sh** command to check the current consumption status.

   -  Check the Consumer Group list on Kafka saved by Offset:

      **./kafka-consumer-groups.sh --list --bootstrap-server** <*Service IP address of any broker node:21007*> **--command-config ../config/consumer.properties**

      eg:./kafka-consumer-groups.sh --bootstrap-server 192.168.1.1:21007 --list --command-config ../config/consumer.properties

   -  Check the consumption status of Consumer Group on Kafka saved by Offset:

      **./kafka-consumer-groups.sh --describe --bootstrap-server** <*Service IP address of any broker node:21007*> *--group Consumer group name* **--command-config ../config/consumer.properties**

      eg:./kafka-consumer-groups.sh --describe --bootstrap-server 192.168.1.1:21007 --group example-group --command-config ../config/consumer.properties

   .. important::

      a. Ensure that the current consumer is online and consumes data.
      b. Configure the **group.id** in the **consumer.properties** configuration file and **--group** in the command to the group to be queried.
      c. The Kafka cluster's IP port number is 21007 in security mode and 9092 in normal mode.
