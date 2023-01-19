:original_name: mrs_01_24137.html

.. _mrs_01_24137:

Migrating a Partition on Kafka UI
=================================

Scenario
--------

Migrate a partition on Kafka UI.

.. note::

   -  In security mode, the user who migrates a partition must belong to the **kafkaadmin** user group. Otherwise, the operation fails due to authentication failure.
   -  In non-security mode, Kafka UI does not authenticate any operation.

Migrating a Partition
---------------------

#. Log in to Kafka UI. For details, see :ref:`Accessing Kafka UI <mrs_01_24134>`. Click **Generate assignment**. The **Generate Partition Assignments** page is displayed.

#. In the **Brokers** area, select brokers to which the topic is to be re-assigned.

#. Click **Generate Partition Assignments** to generate a partition migration solution.

   |image1|

#. Click **Run assignment** to migrate a partition.

.. |image1| image:: /_static/images/en-us_image_0000001349139497.png
