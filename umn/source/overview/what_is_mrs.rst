:original_name: mrs_08_0001.html

.. _mrs_08_0001:

What Is MRS?
============

Big data is a huge challenge facing the Internet era as the data volume and types increase rapidly. Conventional data processing technologies, such as single-node storage and relational databases, are unable to solve the emerging big data problems. In this case, the Apache Software Foundation (ASF) has launched an open source Hadoop big data processing solution. Hadoop is an open source distributed computing platform that can fully utilize computing and storage capabilities of clusters to process massive amounts of data. If enterprises deploy Hadoop systems by themselves, the disadvantages include high costs, long deployment period, difficult maintenance, and inflexible use.

To solve the preceding problems, the cloud provides MapReduce Service (MRS) for managing the Hadoop system. With MRS, you can deploy a Hadoop cluster in just one click. MRS provides enterprise-level big data clusters on the cloud. Tenants can fully control clusters and easily run big data components such as Storm, Hadoop, Spark, HBase, and Kafka. MRS is fully compatible with open source APIs, and incorporates advantages of the cloud computing and storage and big data industry experience to provide customers with a full-stack big data platform featuring high performance, low cost, flexibility, and ease-of-use. In addition, the platform can be customized based on service requirements to help enterprises quickly build a massive data processing system and discover new value points and business opportunities by analyzing and mining massive amounts of data in real time or in non-real time.

Product Architecture
--------------------

:ref:`Figure 1 <mrs_08_0001__fig1150416195911>` shows the MRS logical architecture.

.. note::

   MRS 3.x or later does not support patch management on the management console.

.. _mrs_08_0001__fig1150416195911:

.. figure:: /_static/images/en-us_image_0000001441155405.png
   :alt: **Figure 1** MRS architecture

   **Figure 1** MRS architecture

MRS architecture includes infrastructure and big data processing phases.

-  Infrastructure

   MRS big data clusters are built based on Elastic Cloud Server (ECS), and make full use of the high reliability and security capabilities of the virtualization layer.

   -  A Virtual Private Cloud (VPC) is a virtual internal network provided for each tenant. It is isolated from other networks by default.
   -  Elastic Volume Service (EVS) provides highly reliable and high-performance storage.
   -  ECS provides scalable VMs, and works with VPCs, security groups, and the EVS multi-replica mechanism to build an efficient, reliable, and secure computing environment.

-  Data collection

   The data collection layer provides the capability of importing data from various dta sources, such as Flume (data ingestion), Loader (relational data import), and Kafka (highly reliable message queue), to MRS big data clusters. Alternatively, you can use Cloud Data Migration (CDM) to import external data to MRS clusters.

-  Data storage

   MRS clusters can store structured and unstructured data, and support multiple efficient formats to meet the requirements of different computing engines.

   -  HDFS is a general-purpose distributed file system on a big data platform.
   -  OBS is an object storage service that features high availability and low cost.
   -  HBase supports data storage with indexes, and is applicable to high-performance index-based query scenarios.

-  Data convergence processing

   -  MRS provides multiple mainstream compute engines, including MapReduce (batch processing), Tez (DAG model), Spark (in-memory computing), Spark Streaming (micro-batch stream computing), Storm (stream computing), and Flink (stream computing), to convert data structures and logic into data models that meet service requirements in a variety of big data application scenarios.
   -  Based on the preset data model and easy-to-use SQL data analysis, users can select Hive (data warehouse), SparkSQL, and Presto (interactive query engine).

-  Data display and scheduling

   Displays data analysis results and integrates with Data Lake Governance Center (DGC) to provide a one-stop big data collaborative development platform, helping you easily complete multiple tasks, such as data modeling, data integration, script development, job scheduling, and O&M monitoring, making big data more accessible than ever before, and helping you effortlessly build big data processing centers.

-  Cluster management

   All components of the Hadoop-based big data ecosystem are deployed in distributed mode, and their deployment, management, and O&M are complex.

   MRS provides a unified O&M management platform for cluster management, supporting one-click cluster deployment, multi-version selection, as well as manual scaling and auto scaling of clusters without service interruption. In addition, MRS provides job management, resource tag management, and O&M of the preceding data processing components at each layer. It also provides one-stop O&M capabilities, covering monitoring, alarm reporting, configuration, and patch upgrade.

Product Advantages
------------------

MRS has a powerful Hadoop kernel team and is deployed based on enterprise-level FusionInsight big data platform. MRS has been deployed on tens of thousands of nodes and can ensure Service Level Agreements (SLAs) for multi-level users.

MRS has the following advantages:

-  High performance

   MRS supports self-developed CarbonData storage technology. CarbonData is a high-performance big data storage solution. It allows one data set to apply to multiple scenarios and supports features, such as multi-level indexing, dictionary encoding, pre-aggregation, dynamic partitioning, and quasi-real-time data query. This improves I/O scanning and computing performance and returns analysis results of tens of billions of data records in seconds. In addition, MRS supports self-developed enhanced scheduler Superior, which breaks the scale bottleneck of a single cluster and is capable of scheduling over 10,000 nodes in a cluster.

-  Cost-effectiveness

   Based on diversified cloud infrastructure, MRS provides various computing and storage choices and separates computing from storage, delivering cost-effective massive data storage solutions. MRS supports auto scaling to address peak and off-peak service loads, releasing idle resources on the big data platform for customers. MRS clusters can be created and scaled out when you need them, and can be terminated or scaled in after you use them, minimizing cost.

-  High security

   MRS delivers enterprise-level big data multi-tenant permissions management and security management to support table-based and column-based access control and data encryption.

-  Easy O&M

   MRS provides a visualized big data cluster management platform, improving O&M efficiency. MRS supports rolling patch upgrade and provides visualized patch release information and one-click patch installation without manual intervention, ensuring long-term stability of user clusters.

-  High reliability

   The proven large-scale reliability and long-term stability of MRS meet enterprise-level high reliability requirements. In addition, MRS supports automatic data backup across AZs and regions, as well as automatic anti-affinity. It allows VMs to be distributed on different physical machines.
