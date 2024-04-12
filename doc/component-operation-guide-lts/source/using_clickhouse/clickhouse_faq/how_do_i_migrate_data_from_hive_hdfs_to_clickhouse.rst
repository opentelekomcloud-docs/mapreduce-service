:original_name: mrs_01_24831.html

.. _mrs_01_24831:

How Do I Migrate Data from Hive/HDFS to ClickHouse?
===================================================

Question
--------

How do I migrate Hive/HDFS data to ClickHouse?

Answer
------

You can export data from Hive as CSV files and import the CSV files to ClickHouse.

#. Export data from Hive as CSV files.

   **hive -e "select \* from db_hive.student limit 1000"\| tr "\\t" "," > /data/bigdata/hive/student.csv;**

#. Import the CSV files to the **student_hive** table in the default database of ClickHouse.

   **clickhouse --client --port 9002 --password password -m --query='INSERT INTO default.student_hive FORMAT CSV' < /data/bigdata/hive/student.csv**
