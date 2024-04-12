:original_name: mrs_01_24206.html

.. _mrs_01_24206:

Using ClickHouse to Import and Export Data
==========================================

Using the ClickHouse Client to Import and Export Data
-----------------------------------------------------

Use the ClickHouse client to import and export data.

-  Importing data in CSV format

   **clickhouse client --host** *Host name or IP address of the ClickHouse instance* **--database** *Database name* **--port** *Port number* **--secure --format_csv_delimiter="**\ *CSV file delimiter*\ **" --query="INSERT INTO** *Table name* **FORMAT CSV" <** *Host path where the CSV file is stored*

   Example

   .. code-block::

      clickhouse client --host 10.5.208.5 --database testdb --port 9440 --secure --format_csv_delimiter="," --query="INSERT INTO testdb.csv_table FORMAT CSV" < /opt/data

   You need to create a table in advance.

-  Exporting data in CSV format

   .. caution::

      Exporting data files in CSV format may cause CSV injection. Exercise caution when performing this operation.

   **clickhouse client --host** *Host name or IP address of the ClickHouse instance* **--database** *Database name* **--port** *Port number* **-m --secure --query=**"SELECT \* **FROM** *Table name*" > *CSV file export path*

   Example

   .. code-block::

      clickhouse client --host 10.5.208.5 --database testdb --port 9440 -m --secure --query="SELECT * FROM test_table" > /opt/test

-  Importing data in Parquet format

   **cat** *Parquet file* **\| clickhouse client --host** *Host name or IP address of the ClickHouse instance* **--database** *Database name* **--port** *Port number* **-m --secure --query="INSERT INTO** *Table name* **FORMAT Parquet"**

   Example

   .. code-block::

      cat /opt/student.parquet | clickhouse client --host 10.5.208.5 --database testdb --port 9440 -m --secure --query="INSERT INTO parquet_tab001 FORMAT Parquet"

-  Exporting data in Parquet format

   **clickhouse client --host** *Host name or IP address of the ClickHouse instance* **--database** *Database name* **--port** *Port number* **-m --secure --query=**"**select** \* **from** *Table name* **FORMAT Parquet**" > *Parquet file export path*

   Example

   .. code-block::

      clickhouse client --host 10.5.208.5 --database testdb --port 9440 -m --secure --query="select * from test_table FORMAT Parquet" > /opt/student.parquet

-  Importing data in ORC format

   **cat** *ORC file path* **\| clickhouse client --host** *Host name or IP address of the ClickHouse instance* **--database** *Database name* **--port** *Port number* **-m --secure --query=**"**INSERT INTO** *Table name* **FORMAT ORC**"

   Example

   .. code-block::

      cat /opt/student.orc | clickhouse client --host 10.5.208.5 --database testdb --port 9440 -m --secure --query="INSERT INTO orc_tab001 FORMAT ORC"
      # Data in the ORC file can be exported from HDFS. For example:
      hdfs dfs -cat /user/hive/warehouse/hivedb.db/emp_orc/000000_0_copy_1 | clickhouse client --host 10.5.208.5 --database testdb --port 9440 -m --secure --query="INSERT INTO orc_tab001 FORMAT ORC"

-  Exporting data in ORC format

   **clickhouse client --host** *Host name or IP address of the ClickHouse instance* **--database** *Database name* **--port** *Port number* **-m** **--secure --query=**"**select** \* **from** *Table name* **FORMAT ORC**" > *ORC file export path*

   Example

   .. code-block::

      clickhouse client --host 10.5.208.5 --database testdb --port 9440 -m --secure --query="select * from csv_tab001 FORMAT ORC" > /opt/student.orc

-  Importing data in JSON format

   **INSERT INTO** *Table name* **FORMAT JSONEachRow** *JSON string* *1* *JSON string 2*

   Example

   .. code-block::

      INSERT INTO test_table001 FORMAT JSONEachRow {"PageViews":5, "UserID":"4324182021466249494", "Duration":146,"Sign":-1} {"UserID":"4324182021466249494","PageViews":6,"Duration":185,"Sign":1}

-  Exporting data in JSON format

   **clickhouse client --host** *Host name or IP address of the ClickHouse instance* **--database** *Database name* **--port** *Port number* **-m --secure --query=**"**SELECT** \* **FROM** *Table name* **FORMAT JSON|JSONEachRow|JSONCompact|...**" > *JSON file export path*

   Example

   .. code-block::

      # Export JSON file.
      clickhouse client --host 10.5.208.5 --database testdb --port 9440 -m --secure --query="SELECT * FROM test_table FORMAT JSON" > /opt/test.json

      # Export json(JSONEachRow).
      clickhouse client --host 10.5.208.5 --database testdb --port 9440 -m --secure --query="SELECT * FROM test_table FORMAT JSONEachRow" > /opt/test_jsoneachrow.json

      # Export json(JSONCompact).
      clickhouse client --host 10.5.208.5 --database testdb --port 9440 -m --secure --query="SELECT * FROM test_table FORMAT JSONCompact" > /opt/test_jsoncompact.json
