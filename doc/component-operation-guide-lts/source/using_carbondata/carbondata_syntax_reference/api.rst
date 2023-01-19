:original_name: mrs_01_1450.html

.. _mrs_01_1450:

API
===

This section describes the APIs and usage methods of Segment. All methods are in the org.apache.spark.util.CarbonSegmentUtil class.

The following methods have been abandoned:

.. code-block::

   /**
   * Returns the valid segments for the query based on the filter condition
   * present in carbonScanRdd.
   *
   * @param carbonScanRdd
   * @return Array of valid segments
   */
   @deprecated def getFilteredSegments(carbonScanRdd: CarbonScanRDD[InternalRow]): Array[String];

Usage Method
------------

Use the following methods to obtain CarbonScanRDD from the query statement:

.. code-block::

   val df=carbon.sql("select * from table where age='12'")
   val myscan=df.queryExecution.sparkPlan.collect {
   case scan: CarbonDataSourceScan if scan.rdd.isInstanceOf[CarbonScanRDD[InternalRow]] => scan.rdd
   case scan: RowDataSourceScanExec if scan.rdd.isInstanceOf[CarbonScanRDD[InternalRow]] => scan.rdd
   }.head
   val carbonrdd=myscan.asInstanceOf[CarbonScanRDD[InternalRow]]

Example:

.. code-block::

   CarbonSegmentUtil.getFilteredSegments(carbonrdd)

The filtered segment can be obtained by importing SQL statements.

.. code-block::

   /**
   * Returns an array of valid segment numbers based on the filter condition provided in the sql
   * NOTE: This API is supported only for SELECT Sql (insert into,ctas,.., is not supported)
   *
   * @param sql
   * @param sparkSession
   * @return Array of valid segments
   * @throws UnsupportedOperationException because Get Filter Segments API supports if and only
   * if only one carbon main table is present in query.
   */
   def getFilteredSegments(sql: String, sparkSession: SparkSession): Array[String];

Example:

.. code-block::

   CarbonSegmentUtil.getFilteredSegments("select * from table where age='12'", sparkSession)

Import the database name and table name to obtain the list of segments to be merged. The obtained segments can be used as parameters of the getMergedLoadName function.

.. code-block::

   /**
   * Identifies all segments which can be merged with MAJOR compaction type.
   * NOTE: This result can be passed to getMergedLoadName API to get the merged load name.
   *
   * @param sparkSession
   * @param tableName
   * @param dbName
   * @return list of LoadMetadataDetails
   */
   def identifySegmentsToBeMerged(sparkSession: SparkSession,
   tableName: String,
   dbName: String) : util.List[LoadMetadataDetails];

Example:

.. code-block::

   CarbonSegmentUtil.identifySegmentsToBeMerged(sparkSession, "table_test","default")

Import the database name, table name, and obtain all segments which can be merged with CUSTOM compaction type. The obtained segments can be transferred as the parameter of the getMergedLoadName function.

.. code-block::

   /**
   * Identifies all segments which can be merged with CUSTOM compaction type.
   *  NOTE: This result can be passed to getMergedLoadName API to get the merged load name.
   *
   * @param sparkSession
   * @param tableName
   * @param dbName
   * @param customSegments
   * @return list of LoadMetadataDetails
   * @throws UnsupportedOperationException if customSegments is null or empty.
   * @throws MalformedCarbonCommandException if segment does not exist or is not valid
   */
   def identifySegmentsToBeMergedCustom(sparkSession: SparkSession,
   tableName: String,
   dbName: String,
   customSegments: util.List[String]): util.List[LoadMetadataDetails];

Example:

.. code-block::

   val customSegments = new util.ArrayList[String]()
   customSegments.add("1")
   customSegments.add("2")
   CarbonSegmentUtil.identifySegmentsToBeMergedCustom(sparkSession, "table_test","default", customSegments)

If a segment list is specified, the merged load name is returned.

.. code-block::

   /**
   * Returns the Merged Load Name for given list of segments
   *
   * @param list of segments
   * @return Merged Load Name
   * @throws UnsupportedOperationException if list of segments is less than 1
   */
   def getMergedLoadName(list: util.List[LoadMetadataDetails]): String;

Example:

.. code-block::

   val carbonTable = CarbonEnv.getCarbonTable(Option(databaseName), tableName)(sparkSession)
   val loadMetadataDetails = SegmentStatusManager.readLoadMetadata(carbonTable.getMetadataPath)  CarbonSegmentUtil.getMergedLoadName(loadMetadataDetails.toList.asJava)
