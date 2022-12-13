:original_name: mrs_08_00671.html

.. _mrs_08_00671:

Oozie Basic Principles
======================

Introduction to Oozie
---------------------

`Oozie <http://oozie.apache.org/>`__ is an open-source workflow engine that is used to schedule and coordinate Hadoop jobs.

Architecture
------------

The Oozie engine is a web application integrated into Tomcat by default. Oozie uses PostgreSQL databases.

Oozie provides an Ext-based web console, through which users can view and monitor Oozie workflows. Oozie provides an external REST web service API for the Oozie client to control workflows (such as starting and stopping operations), and orchestrate and run Hadoop MapReduce tasks. For details, see :ref:`Figure 1 <mrs_08_00671__it_hd_des_000065_mmccppss_fig_01>`.

.. _mrs_08_00671__it_hd_des_000065_mmccppss_fig_01:

.. figure:: /_static/images/en-us_image_0000001296590678.png
   :alt: **Figure 1** Oozie architecture

   **Figure 1** Oozie architecture

:ref:`Table 1 <mrs_08_00671__tab01>` describes the functions of each module shown in :ref:`Figure 1 <mrs_08_00671__it_hd_des_000065_mmccppss_fig_01>`.

.. _mrs_08_00671__tab01:

.. table:: **Table 1** Architecture description

   +-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Connection Name   | Description                                                                                                                                                                                                                        |
   +===================+====================================================================================================================================================================================================================================+
   | Console           | Allows users to view and monitor Oozie workflows.                                                                                                                                                                                  |
   +-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Client            | Controls workflows, including submitting, starting, running, planting, and restoring workflows, through APIs.                                                                                                                      |
   +-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | SDK               | Is short for software development kit. An SDK is a set of development tools used by software engineers to establish applications for particular software packages, software frameworks, hardware platforms, and operating systems. |
   +-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Database          | PostgreSQL database                                                                                                                                                                                                                |
   +-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | WebApp (Oozie)    | Functions as the Oozie server. It can be deployed on a built-in or an external Tomcat container. Information recorded by WebApp (Oozie) including logs is stored in the PostgreSQL database.                                       |
   +-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Tomcat            | A free open-source web application server                                                                                                                                                                                          |
   +-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Hadoop components | Underlying components, such as MapReduce and Hive, that execute the workflows orchestrated by Oozie.                                                                                                                               |
   +-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Principle
---------

Oozie is a workflow engine server that runs MapReduce workflows. It is also a Java web application running in a Tomcat container.

Oozie workflows are constructed using Hadoop Process Definition Language (HPDL). HPDL is an XML-defined language, similar to JBoss jBPM Process Definition Language (jPDL). An Oozie workflow consists of the Control Node and Action Node.

-  Control Node controls workflow orchestration, such as **start**, **end**, **error**, **decision**, **fork**, and **join**.

-  An Oozie workflow contains multiple Action Nodes, such as MapReduce and Java.

   All Action Nodes are deployed and run in Direct Acyclic Graph (DAG) mode. Therefore, Action Nodes run in direction. That is, the next Action Node can run only when the running of the previous Action Node ends. When one Action Node ends, the remote server calls back the Oozie interface. Then Oozie executes the next Action Node of workflow in the same manner until all Action Nodes are executed (execution failures are counted).

Oozie workflows provide various types of Action Nodes, such as MapReduce, Hadoop distributed file system (HDFS), Secure Shell (SSH), Java, and Oozie sub-flows, to support a wide range of business requirements.
