:original_name: mrs_08_00142.html

.. _mrs_08_00142:

Relationship Between Storm and Other Components
===============================================

Storm provides a real-time distributed computing framework. It can obtain real-time messages from data sources (such as Kafka and TCP connection), perform high-throughput and low-latency real-time computing on a real-time platform, and export results to message queues or implement data persistence. :ref:`Figure 1 <mrs_08_00142__fig_re>` shows the relationship between Storm and other components.

.. _mrs_08_00142__fig_re:

.. figure:: /_static/images/en-us_image_0000001349190329.png
   :alt: **Figure 1** Relationship with other components

   **Figure 1** Relationship with other components

Relationship between Storm and Streaming
----------------------------------------

Both Storm and Streaming use the open source Apache Storm kernel. However, the kernel version used by Storm is 1.2.1 whereas that used by Streaming is 0.10.0. Streaming is used to inherit transition services in upgrade scenarios. For example, if Streaming has been deployed in an earlier version and services are running, Streaming can still be used after the upgrade. Storm is recommended in a new cluster.

Storm 1.2.1 has the following new features:

-  **Distributed cache**: Provides external resources (configurations) required for sharing and updating the topology using CLI tools. You do not need to re-package and re-deploy the topology.
-  **Native Streaming Window API**: Provides window-based APIs.
-  **Resource scheduler**: Added the resource scheduler plug-in. When defining a topology, you can specify the maximum resources available and assign resource quotas to users, thus to manage topology resources of the users.
-  **State management**: Provides the Bolt API with the checkpoint mechanism. When an event fails, Storm automatically manages the Bolt status and restore the event.
-  **Message sampling and debugging**: On the Storm UI, you can enable or disable topology- or component-level debugging to output stream messages to specified logs based on the sampling ratio.
-  **Worker dynamic analysis**: On the Storm UI, you can collect jstack and heap logs of the Worker process and restart the Worker process.
-  **Dynamic adjustment of topology logs**: You can dynamically change the running topology logs on the CLI or Storm UI.
-  **Improved performance**: Compared with earlier versions, the performance of Storm is greatly improved. Although the topology performance is closely related to the use case scenario and dependency on external services, the performance is three times higher in most scenarios.
