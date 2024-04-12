:original_name: mrs_01_24789.html

.. _mrs_01_24789:

Enabling the CPU Priority Feature
=================================

.. note::

   This section applies only to MRS 3.2.0 or later.

Scenario
--------

ClickHouse tenants support CPU priorities. This feature depends on CAP_SYS_NICE of the OS and takes effect only after being enabled.

Procedure
---------

#. Log in to the ClickHouseServer node as user **root** and run the following command:

   **setcap cap_sys_nice=+ep /opt/Bigdata/FusionInsight_ClickHouse_*/install/FusionInsight-ClickHouse-*/clickhouse/bin/clickhouse**

   .. note::

      You need to run this command on all ClickHouseServer nodes.

#. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **ClickHouse**. Cick the **Instance** tab. Select all ClickHouseServer instances, and choose **More** > **Restart Instance**.

#. Run the following command to check whether the CPU priority feature is enabled:

   **getcap /opt/Bigdata/FusionInsight_ClickHouse_*/install/FusionInsight-ClickHouse-*/clickhouse/bin/clickhouse**

   The following command output indicates that the feature has been enabled:

   .. code-block::

      /opt/Bigdata/FusionInsight_ClickHouse_*/install/FusionInsight-ClickHouse*/clickhouse/bin/clickhouse = cap_sys_nice+ep

#. (Optional) If the current cluster runs SUSE, run the following command on each ClickHouseServer node:

   **sudo zypper install libcap-progs**
