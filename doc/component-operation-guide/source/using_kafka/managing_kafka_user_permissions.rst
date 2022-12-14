:original_name: mrs_01_0378.html

.. _mrs_01_0378:

Managing Kafka User Permissions
===============================

Scenario
--------

For clusters with Kerberos authentication enabled, using Kafka requires relevant permissions. MRS clusters can grant the use permission of Kafka to different users.

:ref:`Table 1 <mrs_01_0378__t5ed4e7771fac4113ad733d56146a3b07>` lists the default Kafka user groups.

.. note::

   In MRS 3.\ *x* or later, Kafka supports two types of authentication plug-ins: Kafka open source authentication plug-in and Ranger authentication plug-in.

   This section describes the user permission management based on the Kafka open source authentication plug-in. For details about how to use the Ranger authentication plug-in, see :ref:`Adding a Ranger Access Permission Policy for Kafka <mrs_01_1861>`.

.. _mrs_01_0378__t5ed4e7771fac4113ad733d56146a3b07:

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

   -  For versions earlier than MRS 1.9.2, log in to MRS Manager and choose **Services** > **ZooKeeper** > **Instance**.
   -  For MRS 1.9.2 or later to versions earlier than 3.x, click the cluster name on the MRS console and choose **Components** > **ZooKeeper** > **Instances**.

      .. note::

         If the **Components** tab is unavailable, complete IAM user synchronization first. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

#. View the IP addresses of the ZooKeeper role instance.

   Record the IP address of any ZooKeeper instance.

#. Prepare the client based on service requirements. Log in to the node where the client is installed.

#. Run the following command to switch to the client directory, for example, **/opt/client/Kafka/kafka/bin**.

   **cd /opt/client/Kafka/kafka/bin**

#. Run the following command to configure environment variables:

   **source /opt/client/bigdata_env**

#. Run the following command to authenticate the user(skip this step in normal mode):

   **kinit** *Component service user*

#. Versions earlier than MRS 3.x: Select the scenario required by the service and manage Kafka user permissions.

   -  Querying the permission list of a topic

      **sh kafka-acls.sh --authorizer-properties zookeeper.connect=\ IP address of the node where the ZooKeeper instance resides:2181/kafka --list --topic** **Topic name**

   -  Adding producer permission to a user

      **sh kafka-acls.sh --authorizer-properties zookeeper.connect=**\ **IP address of the node where the ZooKeeper instance resides**\ **:2181/kafka --add --allow-principal User:**\ **Username** **--producer --topic** **Topic name**

   -  Removing producer permission of a user

      **sh kafka-acls.sh --authorizer-properties zookeeper.connect=**\ **IP address of the node where the ZooKeeper instance resides**\ **:2181/kafka --remove --allow-principal User:**\ **Username** **--producer --topic** **Topic name**

   -  Adding consumer permission to a user

      **sh kafka-acls.sh --authorizer-properties zookeeper.connect=**\ **IP address of the node where the ZooKeeper instance resides**\ **:2181/kafka --add --allow-principal User:**\ **Username** **--consumer --topic** **Topic name** **--group** **Consumer group name**

   -  Removing consumer permission of a user

      **sh kafka-acls.sh --authorizer-properties zookeeper.connect=**\ **IP address of the node where the ZooKeeper instance resides**\ **:2181/kafka --remove --allow-principal User:**\ **Username** **--consumer --topic** **Topic name** **--group** **Consumer group name**

   .. note::

      You need to enter **y** twice to confirm the removal of permission.

      For MRS 1.6.2 or earlier, the value of ZooKeeper's **clientPort** defaults to **24002**.

#. MRS 3.\ *x* and later versions: The following table lists the common commands used for user authorization when **kafka-acl.sh** is used.

   -  View the permission control list of a topic:

      **./kafka-acls.sh --authorizer-properties zookeeper.connect=**\ *<Service IP address of any ZooKeeper node*\ **:2181/kafka** *>* **--list --topic** *<Topic name>*

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --list --topic** <*topic* *name*>

   -  Add the Producer permission for a user:

      **./kafka-acls.sh --authorizer-properties zookeeper.connect=**\ *<Service IP address of any ZooKeeper node*\ **:2181/kafka > --add --allow-principal User:**\ *<Username>* **--producer --topic** *<Topic name>*

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --add --allow-principal User:**\ *<username>* **--producer --topic** <*topic* *name*>

   -  Assign the Producer permission to a user in batches.

      **./kafka-acls.sh --authorizer-properties zookeeper.connect=**\ *<Service IP address of any ZooKeeper node*\ **:2181/kafka >** **--add --allow-principal User:**\ *<Username>* **--producer --topic** *<Topic name>* **--resource-pattern-type prefixed**

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --add --allow-principal User:**\ *<username>* **--producer --topic** *<topic name>*\ **--resource-pattern-type prefixed**

   -  Remove the Producer permission from a user:

      **./kafka-acls.sh --authorizer-properties zookeeper.connect=**\ *<Service IP adddress of any ZooKeeper node*\ **:2181/kafka > --remove --allow-principal User:**\ *<Username>* **--producer --topic** *<Topic name>*

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --remove --allow-principal User:**\ *<username>* **--producer --topic** <*topic* *name*>

   -  Delete the Producer permission of a user in batches:

      **./kafka-acls.sh --authorizer-properties zookeeper.connect=**\ *<Service IP address of any ZooKeeper node*\ **:2181/kafka >** **--remove --allow-principal User:**\ *<Username>* **--producer --topic** *<Topic name>* **--resource-pattern-type prefixed**

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --remove --allow-principal User:**\ *<username>* **--producer --topic** *<topic name>*\ **--resource-pattern-type prefixed**

   -  Add the Consumer permission for a user:

      **./kafka-acls.sh --authorizer-properties zookeeper.connect=**\ *<Service IP address of any ZooKeeper node*\ **:2181/kafka >** **--add --allow-principal User:**\ *<Username>* **--consumer --topic** *<Topicname>* **--group** *<Consumer group name>*

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --add --allow-principal User:**\ *<username>* **--consumer --topic** *<topicname>* **--group** *<consumer group name>*

   -  Add consumer permissions to a user in batches:

      **./kafka-acls.sh** **--authorizer-properties zookeeper.connect=**\ *<Service IP address of any ZooKeeper node*\ **:2181/kafka >** **--add --allow-principal User:**\ *<Username>* **--consumer --topic** *<Topic* *name>* **--group** *<Consumer group name>* **--resource-pattern-type prefixed**

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --add --allow-principal User:**\ *<username>* **--consumer --topic** *<topicname>* **--group** *<consumer group name>* **--resource-pattern-type prefixed**

   -  Remove the consumer permission from a user:

      **./kafka-acls.sh --authorizer-properties zookeeper.connect=**\ *<Service IP address of any ZooKeeper node*\ **:2181/kafka >** **--remove --allow-principal User:**\ *<Username>* **--consumer --topic** *<Topic* *name>* **--group** *<Consumer group name>*

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --remove --allow-principal User:**\ *<username>* **--consumer --topic** *<topic name>* **--group** *<consumer group name>*

   -  Delete the consumer permission of a user in batches:

      **./kafka-acls.sh** **--authorizer-properties zookeeper.connect=**\ *<Service IP address of any ZooKeeper node*\ **:2181/kafka >** **--remove --allow-principal User:**\ *<Username>* **--consumer --topic** *<Topic* *name>* **--group** *<Consumer group name>* **--resource-pattern-type prefixed**

      **./kafka-acls.sh --bootstrap-server** <*IP address of the Kafkacluster:21007>* **--command-config ../config/client.properties --remove --allow-principal User:**\ *<username>* **--consumer --topic** *<topicname>* **--group** *<consumer group name>* **--resource-pattern-type prefixed**
