:original_name: mrs_02_0005.html

.. _mrs_02_0005:

Concepts
========

-  Domain

   A domain is created upon successful registration with the cloud platform. The domain has full access permissions for all of its cloud services and resources. It can be used to reset user passwords and grant user permissions. The domain is a payment entity and should not be used directly to perform routine management. For security purposes, create users and grant them permissions for routine management.

-  User

   A user is created using a domain to use cloud services. Each user has its own identity credentials (password and access keys).

   The domain username, and password will be required for API authentication.

-  Region

   Regions are geographic areas isolated from each other. Resources are region-specific and cannot be used across regions through internal network connections. For low network latency and quick resource access, select the nearest region.

-  AZ

   An AZ contains one or more physical data centers. Each AZ has independent cooling, fire extinguishing, moisture-proof, and electricity facilities. Within an AZ, computing, network, storage, and other resources are logically divided into multiple clusters. AZs within a region are interconnected using high-speed optical fibers to support cross-AZ high-availability systems.

-  Project

   Projects group and isolate resources (including compute, storage, and network resources) across physical regions. A default project is provided for each region, and sub-projects can be created under each default project. Users can be granted permissions to access all resources in a specific project in your domain. For more refined access control, create sub-projects under a project and create resources in the sub-projects. Users can then be assigned permissions to access only specific resources in the sub-projects.


   .. figure:: /_static/images/en-us_image_0000001829015345.png
      :alt: **Figure 1** Project isolation model

      **Figure 1** Project isolation model

-  Checkpoint

   Checkpoint: When an application consumes data, the latest SN of the consumed data is recorded as a checkpoint. When the data is reconsumed, the consumption can be continued based on this checkpoint.

-  App

   Application: Multiple applications can access data in the same stream. Checkpoints generated for each application are used to record the consumed data in the stream by each application.
