:original_name: admin_guide_000408.html

.. _admin_guide_000408:

Overview
========

SQL engines in the big data field are emerging one after another. In addition to a wide range of solutions, some problems are exposed. For example, the quality of SQL input statements is uneven, SQL problems are difficult to locate, and large SQL statements consume too many resources.

Low-quality SQL statements pose unexpected impacts on the data analysis platform, degrading system performance or platform stability.

.. note::

   This function is supported only by MRS 3.3.0 or later.

Function Description
--------------------

MRS allows you to configure inspection rules for mainstream SQL engines (Hive, Spark, HetuEngine, and ClickHouse). MRS can identify typical large SQL queries and low-quality SQL statements and intercepts them before execution or block them during execution. Users do not need to change how they submit SQL statements or change SQL syntax. Service modifications are not required and inspection is easy to implement.

-  You can configure SQL inspection rules on the UI that also allows you to query and modify the rules.
-  During query response and execution, each SQL engine proactively inspects SQL statements based on the rules.
-  Administrators can select to display hints on, intercept, or block SQL statements. The system logs SQL inspection events in real time for SQL audit. O&M engineers can analyze the logs, evaluate SQL statement quality on the live network, detect target statements, and take effective measures.

SQL inspection rules are classified into the following types:

-  Static interception: The system displays hints on or intercepts SQL statements based on SQL syntax rules.
-  Dynamic interception: The system displays hints on or intercepts SQL statements based on rules of data table statistics and metadata information.
-  Runtime Blocking: The system blocks SQL statements based on system states (such as CPU, memory, and I/O) during the runtime of the SQL statements.

SQL requests that meet the static and dynamic interception rules can be intercepted, and the system gives hints for processing the statements properly. If a SQL request meets the blocking rule, the system blocks the SQL task.

Rules and Restrictions
----------------------

-  A SQL inspection rule can be associated with multiple SQL engines, and different threshold parameters can be configured for each service.
-  A SQL inspection rule can be associated with multiple tenants. A rule takes effect only for associated tenants.
