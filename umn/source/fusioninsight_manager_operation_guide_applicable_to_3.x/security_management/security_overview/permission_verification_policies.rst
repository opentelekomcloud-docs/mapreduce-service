:original_name: admin_guide_000238.html

.. _admin_guide_000238:

Permission Verification Policies
================================

Security Mode
-------------

After a user is authenticated by the big data platform, the system determines whether to verify the user's permission based on the actual permission management configuration to ensure that the user has limited or all permission on resources. If the user does not have the permission for accessing cluster resources, the system administrator must grant the required permission to the user. Otherwise, the user fails to access the resources. The cluster provides permission verification capabilities in both security mode and normal mode. The specific permission items of the components are the same in the two modes.

By default, the Ranger service is installed and Ranger authentication is enabled for a newly installed cluster in security mode. You can set fine-grained security access policies for accessing component resources through the permission plug-in of the component. If Ranger authentication is not required, administrators can manually disable it on the service page. After Ranger authentication is disabled, the system continues to perform permission control based on the role model of FusionInsight Manager when accessing component resources.

In a cluster in security mode, the following components support Ranger authentication: HDFS, YARN, Kafka, Hive, HBase, Storm,, Impala, and Spark2x.

For a cluster upgraded from an earlier version, Ranger authentication is not used by default when users access component resources. The administrator can manually enable Ranger authentication after installing Ranger.

By default, all components in the cluster of the security edition authenticate access. The authentication function cannot be disabled.

Normal Mode
-----------

Different components in a normal cluster use their own native open-source authentication behavior. :ref:`Table 1 <admin_guide_000238__ta45bf66853314ecc850b8e6d38b236e9>` lists detailed permission verification modes.

In a normal cluster, Ranger supports permission control on component resources based on OS users. The following components support Ranger authentication: HBase, HDFS, Hive, Spark2x, and YARN.

.. _admin_guide_000238__ta45bf66853314ecc850b8e6d38b236e9:

.. table:: **Table 1** Component permission verification modes in normal clusters

   +------------+-------------------------+------------------------------------------------+
   | Service    | Permission Verification | Permission Verification Enabling and Disabling |
   +============+=========================+================================================+
   | ClickHouse | Required                | Not supported                                  |
   +------------+-------------------------+------------------------------------------------+
   | Flume      | Not required            | Not supported                                  |
   +------------+-------------------------+------------------------------------------------+
   | HBase      | Not required            | Supported                                      |
   +------------+-------------------------+------------------------------------------------+
   | HDFS       | Required                | Supported                                      |
   +------------+-------------------------+------------------------------------------------+
   | Hive       | Not required            | Not supported                                  |
   +------------+-------------------------+------------------------------------------------+
   | Hue        | Not required            | Not supported                                  |
   +------------+-------------------------+------------------------------------------------+
   | Kafka      | Not required            | Not supported                                  |
   +------------+-------------------------+------------------------------------------------+
   | Loader     | Not required            | Not supported                                  |
   +------------+-------------------------+------------------------------------------------+
   | MapReduce  | Not required            | Not supported                                  |
   +------------+-------------------------+------------------------------------------------+
   | Oozie      | Required                | Not supported                                  |
   +------------+-------------------------+------------------------------------------------+
   | Spark2x    | Not required            | Not supported                                  |
   +------------+-------------------------+------------------------------------------------+
   | Storm      | Not required            | Not supported                                  |
   +------------+-------------------------+------------------------------------------------+
   | YARN       | Not required            | Supported                                      |
   +------------+-------------------------+------------------------------------------------+
   | ZooKeeper  | Required                | Supported                                      |
   +------------+-------------------------+------------------------------------------------+

Condition Priorities of the Ranger Permission Policy
----------------------------------------------------

When configuring a permission policy for a resource, you can configure Allow Conditions, Exclude from Allow Conditions, Deny Conditions, and Exclude from Deny Conditions for the resource, to meet unexpected requirements in different scenarios.

The priorities of different conditions are listed in descending order: Exclude from Deny Conditions > Deny Conditions > Exclude from Allow Conditions > Allow Conditions

The following figure shows the process of determining condition priorities. If the component resource request does not match the permission policy in Ranger, the system rejects the access by default. However, for HDFS and Yarn, the system delivers the decision to the access control layer of the component for determination.

|image1|

For example, if you want to grant the read and write permissions of the **FileA** folder to the **groupA** user group, but the user in the group is not **UserA**, you can add an allowed condition and an exception condition.

.. |image1| image:: /_static/images/en-us_image_0000001392733938.png
