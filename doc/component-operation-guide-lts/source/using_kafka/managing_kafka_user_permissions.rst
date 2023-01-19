:original_name: mrs_01_0378.html

.. _mrs_01_0378:

Managing Kafka User Permissions
===============================

Scenario
--------

For clusters with Kerberos authentication enabled, using Kafka requires relevant permissions. MRS clusters can grant the use permission of Kafka to different users.

:ref:`Table 1 <mrs_01_0378__en-us_topic_0000001173949956_t5ed4e7771fac4113ad733d56146a3b07>` lists the default Kafka user groups.

.. note::

   Kafka supports two types of authentication plug-ins: Kafka open-source authentication plug-in and Ranger authentication plug-in.

   This section describes the user permission management based on the Kafka open source authentication plug-in. For details about how to use the Ranger authentication plug-in, see :ref:`Adding a Ranger Access Permission Policy for Kafka <mrs_01_1861>`.

.. _mrs_01_0378__en-us_topic_0000001173949956_t5ed4e7771fac4113ad733d56146a3b07:

.. table:: **Table 1** Default Kafka user groups

   +----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | User Group     | Description                                                                                                                                                                        |
   +================+====================================================================================================================================================================================+
   | kafkaadmin     | Kafka administrator group. Users in this group have the permissions to create, delete, read, and write all topics, and authorize other users.                                      |
   +----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | kafkasuperuser | Kafka super user group. Users in this group have the permissions to read and write all topics.                                                                                     |
   +----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | kafka          | Kafka common user group. Users in this group can access a topic only when they are granted with the read and write permissions of the topic by a user in the **kafkaadmin** group. |
   +----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Prerequisites
-------------

-  You have installed the Kafka client.
-  A user in the **kafkaadmin** group, for example **admin**, has been prepared.

Procedure
---------

#. Access the ZooKeeper instance page.

   Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > *Name of the desired cluster* > **Services** > **ZooKeeper** > **Instance**.

#. View the IP addresses of the ZooKeeper role instance.

   Record the IP address of any ZooKeeper instance.

#. Prepare the client based on service requirements. Log in to the node where the client is installed.

#. Run the following command to switch to the client directory, for example, **/opt/client/Kafka/kafka/bin**.

   **cd /opt/client/Kafka/kafka/bin**

#. Run the following command to configure environment variables:

   **source /opt/client/bigdata_env**

#. Run the following command to authenticate the user (skip this step in normal mode):

   **kinit** *Component service user*

#. The following table lists the common commands used for user authorization when **kafka-acl.sh** is used.

   -  View the permission control list of a topic:

      **./kafka-acls.sh --authorizer-properties zookeeper.connect=**\ *<service IP address of any ZooKeeper node:2181/kafka >* **--list --topic** *<topicname>*

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --list --topic** <*topic* *name*>

   -  Add the Producer permission for a user:

      **./kafka-acls.sh --authorizer-properties zookeeper.connect=**\ *<service IP address of any ZooKeeper node:2181/kafka >* **--add --allow-principal User:**\ *<username>* **--producer --topic** *<topic* *name>*

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --add --allow-principal User:**\ *<username>* **--producer --topic** <*topic* *name*>

   -  Assign the Producer permission to a user in batches.

      **./kafka-acls.sh --authorizer-properties zookeeper.connect=**\ *<service IP address of any ZooKeeper node:2181/kafka >* **--add --allow-principal User:**\ *<username>* **--producer --topic** *<topic nam,e>* **--resource-pattern-type prefixed**

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --add --allow-principal User:**\ *<username>* **--producer --topic** *<topic name>*\ **--resource-pattern-type prefixed**

   -  Remove the Producer permission from a user:

      **./kafka-acls.sh --authorizer-properties zookeeper.connect=**\ *<service IP address of any ZooKeeper node:2181/kafka >* **--remove --allow-principal User:**\ *<username>* **--producer --topic** *<topic* *name>*

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --remove --allow-principal User:**\ *<username>* **--producer --topic** <*topic* *name*>

   -  Delete the Producer permission of a user in batches:

      **./kafka-acls.sh --authorizer-properties zookeeper.connect=**\ *<service IP address of any ZooKeeper node:2181/kafka >* **--remove --allow-principal User:**\ *<username>* **--producer --topic** *<topic name>* **--resource-pattern-type prefixed**

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --remove --allow-principal User:**\ *<username>* **--producer --topic** *<topic name>*\ **--resource-pattern-type prefixed**

   -  Add the Consumer permission for a user:

      **./kafka-acls.sh --authorizer-properties zookeeper.connect=**\ *<service IP address of any ZooKeeper node:2181/kafka >* **--add --allow-principal User:**\ *<user name>* **--consumer --topic** *<topic* *name>* **--group** *<consumer group name>*

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --add --allow-principal User:**\ *<username>* **--consumer --topic** *<topicname>* **--group** *<consumer group name>*

   -  Add consumer permissions to a user in batches:

      **./kafka-acls.sh** **--authorizer-properties zookeeper.connect=**\ *<service IP address of any ZooKeeper node:2181/kafka >* **--add --allow-principal User:**\ *<username>* **--consumer --topic** *<topic* *name>* **--group** *<consumer group name>* **--resource-pattern-type prefixed**

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --add --allow-principal User:**\ *<username>* **--consumer --topic** *<topicname>* **--group** *<consumer group name>* **--resource-pattern-type prefixed**

   -  Remove the consumer permission from a user:

      **./kafka-acls.sh --authorizer-properties zookeeper.connect=**\ *<service IP address of any ZooKeeper node:2181/kafka >* **--remove --allow-principal User:**\ *<username>* **--consumer --topic** *<topic* *name>* **--group** *<consumer group name>*

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --remove --allow-principal User:**\ *<username>* **--consumer --topic** *<topic name>* **--group** *<consumer group name>*

   -  Delete the consumer permission of a user in batches:

      **./kafka-acls.sh** **--authorizer-properties zookeeper.connect=**\ *<service IP address of any ZooKeeper node:2181/kafka >* **--remove --allow-principal User:**\ *<username>* **--consumer --topic** *<topic* *name>* **--group** *<consumer group name>* **--resource-pattern-type prefixed**

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --remove --allow-principal User:**\ *<username>* **--consumer --topic** *<topicname>* **--group** *<consumer group name>* **--resource-pattern-type prefixed**
