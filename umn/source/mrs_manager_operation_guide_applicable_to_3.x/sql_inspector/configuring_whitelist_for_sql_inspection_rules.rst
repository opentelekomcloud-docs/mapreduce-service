:original_name: mrs_01_300638.html

.. _mrs_01_300638:

Configuring Whitelist for SQL Inspection Rules
==============================================

Scenario
--------

This section describes how to configure MRS cluster to skip the SQL inspection rules for Hive and Spark jobs submitted from JobGateway on MRS Manager.

Notes and Constraints
---------------------

This function applies only to clusters of MRS 3.6.0 or later.

Procedure
---------

#. Log in to MRS Manager as a user with Manager administrator right.

#. Click **Cluster** and choose **SQL Inspector**. The **SQL Inspector** page is displayed.

#. Click **Advanced Configurations**, verify the user password, select the components for which SQL inspection rules are to be skipped, and click **OK**.

   Only the Hive and Spark components support skipping SQL inspection rules.


   .. figure:: /_static/images/en-us_image_0000002586558817.png
      :alt: **Figure 1** Advanced configurations

      **Figure 1** Advanced configurations

#. Then, add **sql.defense.skip=true** to **properties** of HiveSql, HiveScript, SparkSql, and SparkScript jobs submitted through JobGateway. In this way, these jobs can skip the SQL inspection rules configured on Manager.

   For example, if you submit a HiveSql job through the JobGateway job API, the configuration is as follows:

   .. code-block::

      {
          "job_name": "job1",
          "job_type": "HiveSql",
          "arguments": ["select * from student where id not in (select id from student where id not in (1,2,3,4,5));"],
          "properties":{"sql.defense.skip":"true"}
      }
