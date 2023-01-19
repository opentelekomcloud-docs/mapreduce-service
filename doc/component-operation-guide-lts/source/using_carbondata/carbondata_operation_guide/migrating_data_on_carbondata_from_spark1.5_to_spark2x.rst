:original_name: mrs_01_2301.html

.. _mrs_01_2301:

Migrating Data on CarbonData from Spark1.5 to Spark2x
=====================================================

Migration Solution Overview
---------------------------

This migration guides you to migrate the CarbonData table data of Spark 1.5 to that of Spark2x.

.. note::

   Before performing this operation, you need to stop the data import service of the CarbonData table in Spark 1.5 and migrate data to the CarbonData table of Spark2x at a time. After the migration is complete, use Spark2x to perform service operations.

Migration roadmap:

#. Use Spark 1.5 to migrate historical data to the intermediate table.
#. Use Spark2x to migrate data from the intermediate table to the target table and change the target table name to the original table name.
#. After the migration is complete, use Spark2x to operate data in the CarbonData table.

Migration Solution and Commands
-------------------------------

**Migrating Historical Data**

#. Stop the CarbonData data import service, use spark-beeline of Spark 1.5 to view the ID and time of the latest segment in the CarbonData table, and record the segment ID.

   **show segments for table dbname.tablename;**

#. .. _mrs_01_2301__en-us_topic_0000001173470780_li1092003116117:

   Run spark-beeline of Spark 1.5 as the user who has created the original CarbonData table to create an intermediate table in ORC or Parquet format. Then import the data in the original CarbonData table to the intermediate table. After the import is complete, the services of the CarbonData table can be restored.

   Create an ORC table.

   **CREATE TABLE dbname.mid_tablename_orc STORED AS ORC as select \* from dbname.tablename;**

   Create a Parquet table.

   **CREATE TABLE dbname.mid_tablename_parq STORED AS PARQUET as select \* from dbname.tablename;**

   In the preceding command, **dbname** indicates the database name and **tablename** indicates the name of the original CarbonData table.

#. .. _mrs_01_2301__en-us_topic_0000001173470780_li192112311210:

   Run spark-beeline of Spark2x as the user who has created the original CarbonData table. Run the table creation statement of the old table to create a CarbonData table.

   .. note::

      In the statement for creating a new table, the field sequence and type must be the same as those of the old table. In this way, the index column structure of the old table can be retained, which helps avoid errors caused by the use of **select \*** statement during data insertion.

   Run the spark-beeline command of Spark 1.5 to view the table creation statement of the old table: **SHOW CREATE TABLE dbname.tablename;**

   Create a CarbonData table named **dbname.new_tablename**.

#. Run spark-beeline of Spark2x as the user who has created the original CarbonData table to load the intermediate table data in ORC (or PARQUET) format created in :ref:`2 <mrs_01_2301__en-us_topic_0000001173470780_li1092003116117>` to the new table created in :ref:`3 <mrs_01_2301__en-us_topic_0000001173470780_li192112311210>`. This step may take a long time (about 2 hours for 200 GB data). The following uses the ORC intermediate table as an example to describe the command for loading data:

   **insert into dbname.new_tablename select \***

   **from dbname. mid_tablename_orc;**

#. Run spark-beeline of Spark2x as the user who has created the original CarbonData table to query and verify the data in the new table. If the data is correct, change the name of the original CarbonData table and then change the name of the new CarbonData table to the name of the original one.

   **ALTER TABLE dbname.tablename RENAME TO dbname.old_tablename;**

   **ALTER TABLE dbname.new_tablename RENAME TO dbname.tablename;**

#. Complete the migration. In this case, you can use Spark2x to query the new table and rebuild the secondary index.
