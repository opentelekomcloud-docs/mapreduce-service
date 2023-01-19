:original_name: mrs_01_24136.html

.. _mrs_01_24136:

Creating a Topic on Kafka UI
============================

Scenario
--------

Create a topic on Kafka UI.

Creating a Topic
----------------

#. Log in to Kafka UI. For details, see :ref:`Accessing Kafka UI <mrs_01_24134>`.

#. Click **Create Topic**. On the displayed page, configure parameters by referring to :ref:`Table 1 <mrs_01_24136__en-us_topic_0000001219231297_table134890201518>` and click **Create**.

   .. _mrs_01_24136__en-us_topic_0000001219231297_table134890201518:

   .. table:: **Table 1** Topic information

      +--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Parameter          | Description                                                                                                                                            | Remarks               |
      +====================+========================================================================================================================================================+=======================+
      | Topic              | Topic name, which can contain a maximum of 249 characters. Only letters, digits, hyphens (-), and underscores (_) are allowed.                         | Example: **kafka_ui** |
      +--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Partitions         | Number of topic partitions. The value must be greater than or equal to 1. The default value is **3**.                                                  | ``-``                 |
      +--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
      | Replication Factor | Replication factor of a topic. The value ranges from 1 to *N*. *N* indicates the number of brokers in the current cluster. The default value is **2**. | ``-``                 |
      +--------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

   .. note::

      -  You can click **Advanced Options** to set advanced topic parameters based on service requirements. Generally, retain the default values.
      -  In a cluster in security mode, the user who creates a topic must belong to the **kafkaadmin** user group. Otherwise, the topic cannot be created due to authentication failure.
      -  In a cluster in non-security mode, no authentication is required for creating a topic. That is, any user can create a topic.
