:original_name: mrs_08_00681.html

.. _mrs_08_00681:

HetuEngine Product Overview
===========================

This section applies only to MRS 3.1.2-LTS.3.

HetuEngine Description
----------------------

HetuEngine is an in-house high-performance, interactive SQL analysis and data virtualization engine. It seamlessly integrates with the big data ecosystem to implement interactive query of massive amounts of data within seconds, and supports cross-source and cross-domain unified data access to enable one-stop SQL convergence analysis in the data lake, between lakes, and between lakehouses.

HetuEngine Architecture
-----------------------

HetuEngine consists of different modules. :ref:`Figure 1 <mrs_08_00681__fig1249037338>` shows the architecture.

.. _mrs_08_00681__fig1249037338:

.. figure:: /_static/images/en-us_image_0000001440400425.png
   :alt: **Figure 1** HetuEngine architecture

   **Figure 1** HetuEngine architecture

.. table:: **Table 1** Module description

   +---------------------+---------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Module              | Concept             | Description                                                                                                                                                              |
   +=====================+=====================+==========================================================================================================================================================================+
   | Cloud service layer | HetuEngine CLI/JDBC | HetuEngine client, through which the query request is submitted and the results is returned and displayed.                                                               |
   +---------------------+---------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                     | HSBroker            | Service management component of HetuEngine. It manages and verifies compute instances, monitors health status, and performs automatic maintenance.                       |
   +---------------------+---------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                     | HSConsole           | Provides visualized operation GUIs and RESTful APIs for data source information management, compute instance management, and automatic task query.                       |
   +---------------------+---------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                     | HSFabric            | Provides a unified SQL access entry to meet the requirements for high-performing and highly secure data transfer across domains (data centers).                          |
   +---------------------+---------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Engine layer        | Coordinator         | Management node of HetuEngine compute instances. It receives and parses SQL statements, generates and optimizes execution plans, assigns tasks, and schedules resources. |
   +---------------------+---------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                     | Worker              | Work node of HetuEngine compute instances. It provides capabilities such as parallel data pulling from data sources and distributed SQL computing.                       |
   +---------------------+---------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

HetuEngine Application Scenarios
--------------------------------

HetuEngine supports cross-source (multiple data sources, such as Hive, HBase, GaussDB(DWS), Elasticsearch, and ClickHouse) and cross-domain (multiple regions or data centers) quick joint query, especially for interactive quick query of Hive and Hudi data in the Hadoop cluster (MRS).
