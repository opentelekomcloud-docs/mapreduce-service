:original_name: mrs_01_1153.html

.. _mrs_01_1153:

Using Macro Definitions in Configuration Items
==============================================

When creating or editing Loader jobs, users can use macro definitions during parameter configuration. Then the parameters can be automatically changed to corresponding macro values when a job is implemented.

.. note::

   -  The macro definitions take effect in the job only.
   -  Macro definitions can be imported and exported together with an import or export job. If a job uses macro definitions, the exported job includes the macro definitions. Macro definitions are imported by default when a job is imported.
   -  For details about the **dateformat** definition of the first parameter in the time macro dataformat, see **java.text.SimpleDateFormat.java**. The restrictions of the target system must be followed. For example, HDFS/OBS directories do not support special characters.

Macro Definitions of Loader
---------------------------

At present, Loader supports the following time macro definitions by default:

.. table:: **Table 1** Common macro definitions of Loader

   +-----------------------------------------------+------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Name                                          | Result After the Replacement | Description                                                                                                                                                                       |
   +===============================================+==============================+===================================================================================================================================================================================+
   | @{dateformat("yyyy-MM-dd")}@                  | 2016-05-17                   | Indicates the current date.                                                                                                                                                       |
   +-----------------------------------------------+------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | @{dateformat("yyyy-MM-dd HH:mm:ss")}@         | 2016-05-17 16:50:00          | Indicates current date and time                                                                                                                                                   |
   +-----------------------------------------------+------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | @{timestamp()}@                               | 1463476137557                | Indicates milliseconds since 1970.                                                                                                                                                |
   +-----------------------------------------------+------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | @{dateformat("yyyy-MM-dd HH:mm:ss",-7,DAYS)}@ | 2016-05-10 16:50:00          | Indicates the latest seven days (the present time minus seven days).                                                                                                              |
   |                                               |                              |                                                                                                                                                                                   |
   |                                               |                              | The second parameter supports addition and subtraction.                                                                                                                           |
   |                                               |                              |                                                                                                                                                                                   |
   |                                               |                              | The third parameter is a time unit for calculation. According to definitions in the **java.util.concurrent.TimeUnit.java**, time units include DAYS, HOURS, MINUTES, and SECONDS. |
   +-----------------------------------------------+------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

In the following scenarios, parameters can be configured by using macro definitions.

-  Specifying a data directory that is named by the current date

   The parameter is set to **/user/data/inputdate_@{dateformat("yyyy-MM-dd")} @**.

-  Querying data in the latest seven days by using SQL

   .. code-block::

      select * from table where time between '@{dateformat("yyyy-MM-dd HH:mm:ss",-7,DAYS)}@' and '@{dateformat("yyyy-MM-dd HH:mm:ss")}@'

-  Specifying a table that is named by the current date

   The parameter is set to **table_@{dateformat("yyyy-MM-dd")} @parmvalue**.
