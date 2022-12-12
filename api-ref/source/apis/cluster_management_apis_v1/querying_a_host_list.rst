:original_name: mrs_02_0057.html

.. _mrs_02_0057:

Querying a Host List
====================

Function
--------

This API is used to query a host list of a specified cluster.

URI
---

-  Format

   GET /v1.1/{project_id}/clusters/{cluster_id}/hosts

-  Parameter description

   .. table:: **Table 1** URI parameter description

      +------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | Parameter  | Mandatory | Description                                                                                               |
      +============+===========+===========================================================================================================+
      | project_id | Yes       | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
      +------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | cluster_id | Yes       | Cluster ID                                                                                                |
      +------------+-----------+-----------------------------------------------------------------------------------------------------------+

Request
-------

.. table:: **Table 2** Request parameter description

   +-----------------+-----------------+-----------------+-----------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                               |
   +=================+=================+=================+===========================================================+
   | pageSize        | No              | Integer         | Maximum number of clusters displayed on a page            |
   |                 |                 |                 |                                                           |
   |                 |                 |                 | Value range: [1-2147483646]. The default value is **10**. |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------+
   | currentPage     | No              | Integer         | Current page number The default value is **1**.           |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------+

Response
--------

.. table:: **Table 3** Response parameter description

   +-----------------------+-----------------------+---------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                         |
   +=======================+=======================+=====================================================================+
   | total                 | Integer               | Total number of hosts in a list                                     |
   +-----------------------+-----------------------+---------------------------------------------------------------------+
   | hosts                 | Array                 | Host parameters                                                     |
   |                       |                       |                                                                     |
   |                       |                       | For details, see :ref:`Table 4 <mrs_02_0057__table21026630171650>`. |
   +-----------------------+-----------------------+---------------------------------------------------------------------+

.. _mrs_02_0057__table21026630171650:

.. table:: **Table 4** **Hosts** parameter description

   +-----------------------+-----------------------+--------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                  |
   +=======================+=======================+==============================================================+
   | id                    | String                | VM ID                                                        |
   +-----------------------+-----------------------+--------------------------------------------------------------+
   | ip                    | String                | VM IP address                                                |
   +-----------------------+-----------------------+--------------------------------------------------------------+
   | flavor                | String                | VM flavor ID                                                 |
   +-----------------------+-----------------------+--------------------------------------------------------------+
   | type                  | String                | VM type                                                      |
   |                       |                       |                                                              |
   |                       |                       | Currently, MasterNode, CoreNode, and TaskNode are supported. |
   +-----------------------+-----------------------+--------------------------------------------------------------+
   | name                  | String                | VM name                                                      |
   +-----------------------+-----------------------+--------------------------------------------------------------+
   | status                | String                | Current VM state                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------+
   | mem                   | String                | Memory                                                       |
   +-----------------------+-----------------------+--------------------------------------------------------------+
   | cpu                   | String                | Number of CPU cores                                          |
   +-----------------------+-----------------------+--------------------------------------------------------------+
   | root_volume_size      | String                | OS disk capacity                                             |
   +-----------------------+-----------------------+--------------------------------------------------------------+
   | data_volume_type      | String                | Data disk type                                               |
   +-----------------------+-----------------------+--------------------------------------------------------------+
   | data_volume_size      | Integer               | Data disk capacity                                           |
   +-----------------------+-----------------------+--------------------------------------------------------------+
   | data_volume_count     | Integer               | Number of data disks                                         |
   +-----------------------+-----------------------+--------------------------------------------------------------+

Example
-------

-  Example request

   None

-  Example response

   .. code-block::

      {
        "total": 5,
        "hosts": [
          {
            "id": "063d1d47-ae91-4a48-840c-b3cfe4efbcf0",
            "name": "a78e161c-d14f-4b68-8c2d-0219920ce844_node_core_IQhiC",
            "ip": "192.168.0.169",
            "status": "ACTIVE",
            "flavor": "c6.4xlarge.4linux.mrs",
            "type": "Core",
            "mem": "16384",
            "cpu": "8",
            "root_volume_size": "40",
            "data_volume_type": "SATA",
            "data_volume_size": 100,
            "data_volume_count": 1
          },
          {
            "id": "dc5c6208-faa2-4727-a65a-2b1ce235d350",
            "name": "a78e161c-d14f-4b68-8c2d-0219920ce844_node_master1_ASzkl",
            "ip": "192.168.0.156",
            "status": "ACTIVE",
            "flavor": "c2.4xlarge.linux.mrs",
            "type": "Master",
            "mem": "32768",
            "cpu": "16",
            "root_volume_size": "40",
            "data_volume_type": "SATA",
            "data_volume_size": 100,
            "data_volume_count": 1
          },
          {
            "id": "c0ce793d-848b-448a-835b-ea0cac534b09",
            "name": "a78e161c-d14f-4b68-8c2d-0219920ce844_node_core_ANnRN",
            "ip": "192.168.0.243",
            "status": "ACTIVE",
            "flavor": "c6.4xlarge.4linux.mrs",
            "type": "Core",
            "mem": "16384",
            "cpu": "8",
            "root_volume_size": "40",
            "data_volume_type": "SATA",
            "data_volume_size": 100,
            "data_volume_count": 1
          },
          {
            "id": "95c23e43-ef6e-4732-b6ed-a5f1c7779fae",
            "name": "a78e161c-d14f-4b68-8c2d-0219920ce844_node_core_uRRiA",
            "ip": "192.168.0.126",
            "status": "ACTIVE",
            "flavor": "c6.4xlarge.4linux.mrs",
            "type": "Core",
            "mem": "16384",
            "cpu": "8",
            "root_volume_size": "40",
            "data_volume_type": "SATA",
            "data_volume_size": 100,
            "data_volume_count": 1
          },
          {
            "id": "63bdbf75-1133-4a94-8c27-1fa12c8b9e70",
            "name": "a78e161c-d14f-4b68-8c2d-0219920ce844_node_master2_StqFu",
            "ip": "192.168.0.22",
            "status": "ACTIVE",
            "flavor": "c2.4xlarge.linux.mrs",
            "type": "Master",
            "mem": "32768",
            "cpu": "16",
            "root_volume_size": "40",
            "data_volume_type": "SATA",
            "data_volume_size": 100,
            "data_volume_count": 1
          }
        ]
      }

Status Code
-----------

:ref:`Table 5 <mrs_02_0057__table33682380171927>` describes the status code of this API.

.. _mrs_02_0057__table33682380171927:

.. table:: **Table 5** Status code

   =========== ========================================================
   Status Code Description
   =========== ========================================================
   200         The host list information has been successfully queried.
   =========== ========================================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
