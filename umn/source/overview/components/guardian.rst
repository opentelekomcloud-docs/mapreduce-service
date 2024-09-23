:original_name: mrs_08_0159.html

.. _mrs_08_0159:

Guardian
========

Guardian Basic Principles
-------------------------

Guardian is a service that provides temporary authentication credentials for services such as HDFS, Hive, Spark, HBase, Loader and HetuEngine to access OBS in decoupled storage and compute scenarios. The Guardian component needs to be installed only when OBS is connected. Typical features of Guardian include:

-  Provides the capability of obtaining temporary authentication credentials for accessing OBS.
-  Provides fine-grained permission control for accessing OBS.
-  Provides the unified cache refreshing capability for temporary authentication credentials used to access OBS.

The Guardian server provides functions for the TokenServer role. TokenServer supports multi-instance deployment. Each instance can have the same functions. A single point of failure (SPOF) does not affect service functions. In addition, the Guardian server provides RPC and HTTPS interfaces to obtain temporary authentication credentials for accessing OBS.

Guardian Architecture
---------------------

:ref:`Figure 1 <mrs_08_0159__fig1558913712012>` shows the basic architecture of Guardian.

.. _mrs_08_0159__fig1558913712012:

.. figure:: /_static/images/en-us_image_0000002007523933.png
   :alt: **Figure 1** Guardian architecture

   **Figure 1** Guardian architecture

Relationships Between Guardian and Other Components
---------------------------------------------------

Before accessing OBS, HDFS, Hive, Spark, Flink, HBase, Loader, and HetuEngine access Guardian to obtain temporary credentials for the access. Guardian generates a temporary credential with fine-grained authentication content based on the IAM access request of the current login user and returns the credential to the component. The component uses the credential to access OBS. OBS determines whether the current user has the access permission based on the credential.


.. figure:: /_static/images/en-us_image_0000001971003602.png
   :alt: **Figure 2** Relationships between Guardian and other components

   **Figure 2** Relationships between Guardian and other components
