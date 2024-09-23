:original_name: admin_guide_000414.html

.. _admin_guide_000414:

Configuring Spark SQL Inspection
================================

Scenario
--------

You can configure rules for Spark SQL inspection on FusionInsight Manager and configure rule parameters as you need.

Prerequisites
-------------

-  The cluster client that contains the Spark service has been installed in the **/opt/hadoopclient** directory.
-  Spark is running properly.
-  A tenant, for example, **sparkstatic1** has been added to **Tenant Resources**. For details, see :ref:`Creating Tenants <admin_guide_000100>`.
-  For a cluster with Kerberos authentication enabled, a service user has been created, for example, user **sparkuser**. The user belongs to groups **hive**, **hadoop**, and **supergroup**, the primary group is **hive**, and the bound role is set to **sparkstatic1**.

Constraints
-----------

-  The default dynamic validity period of a rule is 6 minutes.
-  Only SQL jobs are supported.
-  Interception and blocking rules will interrupt SQL queries, so you need to set parameters of these rules properly based on the site requirements.
-  The static rule static_0007 is not required for Spark because it has a Cartesian product restriction (controlled by **spark.sql.crossJoin.enabled**, which is **true** by default). If the spark parameter is **false**, the static_0007 rule will not take effect.
-  Dynamic rules do work on carbon tables.
-  The dynamic rule dynamic_0002 supports SELECT, ALTER TABLE ADD PARTITION and ALTER TABLE DROP PARTITION. If you use a batch deletion statement that contains judgment conditions, for example, ALTER TABLE DROP PARTITION (pt < 10), the statement will be intercepted before the dynamic_0002 rule because the number of partitions is limited by **spark.sql.dropPartitionsInBatch.limit**, which is defaulted to **1000**.
-  Blocking rules has execution latency. For example, if the running_0004 rule is used and the threshold of the scanned data volume is 10 GB, the statement may be blocked when the data volume is 15 GB or higher due to the determination period and task concurrency.
-  If a job does not exceed the threshold until the last several tasks are complete before the block action is triggered, the job cannot be canceled.
-  Blocking rule running_0004: The SQL execution duration includes the execution duration on the Driver side and the job running duration. When the SQL execution is blocked on the Driver side, the job cannot be canceled even if the execution duration exceeds the value of interruption threshold. This problem may occur when INSERT OVERWRITE is performed on a large number of partitions where storage and compute are decoupled.

Procedure
---------

#. Log in to FusionInsight Manager, click **Cluster**, and choose **SQL Inspector**. The **SQL Inspector** page is displayed.

#. .. _admin_guide_000414__en-us_topic_0000001625860966_li7650134142117:

   Add rules for Spark by referring to :ref:`Adding an SQL Inspection <admin_guide_000409>`.

   For details about the rules supported by the Spark SQL engine, see :ref:`MRS SQL Inspection Rules <admin_guide_000409__en-us_topic_0000001662442869_section19510043143814>`.

   For example, add a rule whose ID is **static_0001** to check whether count distinct appears more than two times in the SQL statement. If so, the system displays a hint.


   .. figure:: /_static/images/en-us_image_0000001971077934.png
      :alt: **Figure 1** Adding a Spark SQL inspection rule

      **Figure 1** Adding a Spark SQL inspection rule

#. Log in to the node where the Spark client is installed and run the following command to switch to the client installation directory.

   **cd /opt/hadoopclient**

   Run the following command to set environment variables:

   **source bigdata_env**

   **source Spark/component_env**

#. Perform user authentication for clusters in security mode (Kerberos authentication enabled). Skip this step for clusters in normal mode (Kerberos authentication disabled).

   **kinit** *Spark operation user*

   Example:

   **kinit** **sparkuser**

   Enter the password as prompted and change the password upon your first login.

#. Run the following command to log in to the spark-sql client:

   **cd opt/client/Spark/spark/bin**

   **./spark-sql**

#. Run the following SQL statement on the client to check whether the current rule takes effect:

   Run the following statement to create a table:

   **create table table1(id int, name string) stored as parquet**

   Run the following statement to query data:

   **select count(distinct id),count(distinct id),count(distinct id),count(distinct id),count(distinct id),count(distinct id) from table1;**

   If the number of times count distinct appears in the statement exceeds the threshold configured in :ref:`2 <admin_guide_000414__en-us_topic_0000001625860966_li7650134142117>`, the following information is displayed:

   .. code-block::

      WARNING:  static_0001 Occurrence num of 'COUNT(DISTINCT)'(6) reaches the hint threshold(2)

   If the action set in the rule is **Intercept**, the following information is displayed:

   .. code-block::

      Error in query: static_0001 Occurrence num of 'COUNT(DISTINCT)'(6) reaches the intercept threshold(2)

   In Spark Beeline, you can obtain SQL inspection details from logs.

   a. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Yarn**. On the **Dashboard** page, click the link next to **ResourceManager WebUI** to enter the Yarn web UI.

   b. Click the ID of the target application on the **All Applications** page. The application details page is displayed.

      |image1|

   c. Click **Logs** of the application. On the displayed page, click **stdout** logs to view SQL inspection details.

      |image2|

      |image3|

      |image4|

   .. note::

      a. For more Spark SQL inspection rules, see :ref:`MRS SQL Inspection Rules <admin_guide_000409__en-us_topic_0000001662442869_section19510043143814>`.
      b. You can view query info in the **/opt/hadoopclient/Spark/spark/audit/query.log** path if you are using the Spark client. The log contains detailed running information and the corresponding SQL inspection information.

.. |image1| image:: /_static/images/en-us_image_0000001971237702.png
.. |image2| image:: /_static/images/en-us_image_0000002007717737.png
.. |image3| image:: /_static/images/en-us_image_0000002007758277.png
.. |image4| image:: /_static/images/en-us_image_0000001971077942.png
