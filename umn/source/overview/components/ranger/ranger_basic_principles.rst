:original_name: mrs_08_00411.html

.. _mrs_08_00411:

Ranger Basic Principles
=======================

`Apache Ranger <https://ranger.apache.org/>`__ offers a centralized security management framework and supports unified authorization and auditing. It manages fine grained access control over Hadoop and related components, such as Storm, HDFS, Hive, HBase, and Kafka. You can use the front-end web UI console provided by Ranger to configure policies to control users' access to these components.

:ref:`Figure 1 <mrs_08_00411__fig3876155913592>` shows the Ranger architecture.

.. _mrs_08_00411__fig3876155913592:

.. figure:: /_static/images/en-us_image_0000001349190301.png
   :alt: **Figure 1** Ranger structure

   **Figure 1** Ranger structure

.. table:: **Table 1** Architecture description

   +-----------------+------------------------------------------------------------------------------------------------------------------------------+
   | Connection Name | Description                                                                                                                  |
   +=================+==============================================================================================================================+
   | RangerAdmin     | Provides a WebUI and RESTful API to manage policies, users, and auditing.                                                    |
   +-----------------+------------------------------------------------------------------------------------------------------------------------------+
   | UserSync        | Periodically synchronizes user and user group information from an external system and writes the information to RangerAdmin. |
   +-----------------+------------------------------------------------------------------------------------------------------------------------------+
   | TagSync         | Periodically synchronizes tag information from the external Atlas service and writes the tag information to RangerAdmin.     |
   +-----------------+------------------------------------------------------------------------------------------------------------------------------+

Ranger Principles
-----------------

-  Ranger Plugins

   Ranger provides policy-based access control (PBAC) plug-ins to replace the original authentication plug-ins of the components. Ranger plug-ins are developed based on the authentication interface of the components. Users set permission policies for specified services on the Ranger web UI. Ranger plug-ins periodically update policies from the RangerAdmin and caches them in the local file of the component. When a client request needs to be authenticated, the Ranger plug-in matches the user carried in the request with the policy and then returns an accept or reject message.

-  UserSync User Synchronization

   UserSync periodically synchronizes data from LDAP/Unix to RangerAdmin. In security mode, data is synchronized from LDAP. In non-security mode, data is synchronized from Unix. By default, the incremental synchronization mode is used. In each synchronization period, UserSync updates only new or modified users and user groups. When a user or user group is deleted, UserSync does not synchronize the change to RangerAdmin. That is, the user or user group is not deleted from the RangerAdmin. To improve performance, UserSync does not synchronize user groups to which no user belongs to RangerAdmin.

-  Unified auditing

   Ranger plug-ins can record audit logs. Currently, audit logs can be stored in local files.

-  High reliability

   Ranger supports two RangerAdmins working in active/active mode. Two RangerAdmins provide services at the same time. If either RangerAdmin is faulty, Ranger continues to work.

-  High performance

   Ranger provides the Load-Balance capability. When a user accesses Ranger WebUI using a browser, the Load-Balance automatically selects the RangerAdmin with the lightest load to provide services.
