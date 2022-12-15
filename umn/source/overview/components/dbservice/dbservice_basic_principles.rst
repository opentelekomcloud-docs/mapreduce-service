:original_name: mrs_08_00601.html

.. _mrs_08_00601:

DBService Basic Principles
==========================

Overview
--------

DBService is a HA storage system for relational databases, which is applicable to the scenario where a small amount of data (about 10 GB) needs to be stored, for example, component metadata. DBService can only be used by internal components of a cluster and provides data storage, query, and deletion functions.

DBService is a basic component of a cluster. Components such as Hive, Hue, Oozie, Loader, and Redis, and Loader store their metadata in DBService, and provide the metadata backup and restoration functions by using DBService.

DBService Architecture
----------------------

DBService in the cluster works in active/standby mode. Two DBServer instances are deployed and each instance contains three modules: HA, Database, and FloatIP.

:ref:`Figure 1 <mrs_08_00601__fig12670195704016>` shows the DBService logical architecture.

.. _mrs_08_00601__fig12670195704016:

.. figure:: /_static/images/en-us_image_0000001349390605.png
   :alt: **Figure 1** DBService architecture

   **Figure 1** DBService architecture

:ref:`Table 1 <mrs_08_00601__table51425253145337>` describes the modules shown in :ref:`Figure 1 <mrs_08_00601__fig12670195704016>`

.. _mrs_08_00601__table51425253145337:

.. table:: **Table 1** Module description

   +----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Name     | Description                                                                                                                                                                                                         |
   +==========+=====================================================================================================================================================================================================================+
   | HA       | HA management module. The active/standby DBServer uses the HA module for management.                                                                                                                                |
   +----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Database | Database module. This module stores the metadata of the Client module.                                                                                                                                              |
   +----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | FloatIP  | Floating IP address that provides the access function externally. It is enabled only on the active DBServer instance and is used by the Client module to access Database.                                           |
   +----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Client   | Client using the DBService component, which is deployed on the component instance node. The client connects to the database by using FloatIP and then performs metadata adding, deleting, and modifying operations. |
   +----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
