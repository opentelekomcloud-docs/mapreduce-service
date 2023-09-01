:original_name: mrs_08_0099.html

.. _mrs_08_0099:

Relationship Between CDL and Other Components
=============================================

The CDL component is based on the Kafka Connect framework. Captured data is forwarded using Kafka topics. Therefore, the CDL component depends on the Kafka component. In addition, the CDL component stores task metadata and monitoring information that are also stored in a database. Therefore, the CDL component also depends on the DBService component.
