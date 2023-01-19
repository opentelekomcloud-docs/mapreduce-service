:original_name: mrs_01_1584.html

.. _mrs_01_1584:

ACL Control
===========

In HA mode of Flink, ZooKeeper can be used to manage clusters and discover services. Zookeeper supports SASL ACL control. Only users who have passed the SASL (Kerberos) authentication have the permission to operate files on ZooKeeper. To enable SASL ACL control, perform following configurations in the Flink configuration file.

.. code-block::

   high-availability.zookeeper.client.acl: creator
   zookeeper.sasl.disable: false

For details about configuration items, see :ref:`Table 1 <mrs_01_1575__en-us_topic_0000001219230485_ta903d6a9c6d24f72abdf46625096cd8c>`.
