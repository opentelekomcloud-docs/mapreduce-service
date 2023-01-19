:original_name: mrs_01_24050.html

.. _mrs_01_24050:

How Do I Do If Coordinators and Workers Cannot Be Started on the New Node?
==========================================================================

Question
--------

A new host is added to the cluster in security mode, the NodeManager instance is added, and the parameters of the HetuEngine compute instance are adjusted. After the HetuEngine compute instance is restarted, the Coordinators and Workers of the HetuEngine compute instance cannot be started on the new host.

Answer
------

In security mode, the internal communication between nodes of HetuEngine compute instances uses the Simple and Protected GSS API Negotiation Mechanism (SPNEGO) authentication. The JKS certificate is required. It contains information about all nodes in the compute instance. The information about the newly added nodes is not contained in the original certificate. You need to restart all HetuEngine HSBroker instances to generate a new certificate, and then restart the HetuEngine compute instance.
