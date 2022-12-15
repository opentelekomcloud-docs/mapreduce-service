:original_name: mrs_01_0511.html

.. _mrs_01_0511:

How to Use MRS
==============

MapReduce Service (MRS) is a cloud service that is used to deploy and manage the Hadoop system and enables one-click Hadoop cluster deployment. MRS provides enterprise-level big data clusters on the cloud. Tenants can fully control the clusters and easily run big data components such as Hadoop, Spark, HBase, Kafka, and Storm in the clusters.

MRS is easy to use. You can execute various tasks and process or store PB-level data using computers connected in a cluster. The procedure of using MRS is as follows:

#. Upload local programs and data files to OBS.
#. Create a cluster by following instructions in :ref:`Creating a Custom Cluster <mrs_01_0513>`. You can choose a cluster type for offline data analysis or stream processing or both, and set ECS instance specifications, instance count, data disk type (common I/O, high I/O, and ultra-high I/O), and components to be installed such as Hadoop, Spark, HBase, Hive, Kafka, and Storm in a cluster. You can use a :ref:`bootstrap action <mrs_01_0414>` to execute a script on a specified node before or after the cluster is started to install additional third-party software, modify the cluster running environment, and perform other customizations.
#. :ref:`Manage jobs <mrs_01_0051>`. MRS provides a platform for executing programs you develop. You can submit, execute, and monitor such programs on MRS.
#. :ref:`Manage clusters <en-us_topic_0012808231>`. MRS provides you with MRS Manager, an enterprise-level unified management platform of big data clusters, helping you quickly know health status of services and hosts. Through graphical metric monitoring and customization, you can obtain critical system information in a timely manner. In addition, you can modify service attribute configurations based on service performance requirements, and start or stop clusters, services, and role instances in one click.
#. :ref:`Terminate a cluster <mrs_01_0042>`. You can terminate an MRS cluster that is no longer use after job execution is complete.
