:original_name: mrs_01_2334.html

.. _mrs_01_2334:

Introduction to HetuEngine Cross-Domain Function
================================================

HetuEngine provide unified standard SQL to implement efficient access to multiple data sources distributed in multiple regions (or data centers), shields data differences in the structure, storage, and region, and decouples data and applications.


.. figure:: /_static/images/en-us_image_0000001349139853.png
   :alt: **Figure 1** HetuEngine cross-region functions

   **Figure 1** HetuEngine cross-region functions

Key Technologies and Advantages of HetuEngine Cross-Domain Function
-------------------------------------------------------------------

-  No single-point failure bottleneck: HSFabric supports horizontal scale-out and multi-channel parallel transmission, maximizing the transmission rate. Cross-domain latency is no longer a bottleneck.
-  Better computing resource utilization: Data compression and serialization tasks are delivered to Worker for parallel computing.
-  Efficient serialization: The data serialization format is optimized to reduce the amount of data to be transmitted at the same data volume level.
-  Streaming transmission: Based on HTTP 2.0 stream, ensure the universality of the HTTP protocol and reduce the repeated invoking of RPC during the transmission of a large amount of data.
-  Resumable transmission: A large amount of data is prevented from being retransmitted after the connection is interrupted abnormally during data transmission.
-  Traffic control: The network bandwidth occupied by data transmission can be limited by region to prevent other services from being affected due to exclusive traffic occupation in cross-region limited bandwidth scenarios.
