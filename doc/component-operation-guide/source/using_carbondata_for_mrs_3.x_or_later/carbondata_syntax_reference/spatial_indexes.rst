:original_name: mrs_01_1451.html

.. _mrs_01_1451:

Spatial Indexes
===============

Quick Example
-------------

.. code-block::

   create table IF NOT EXISTS carbonTable
   (
   COLUMN1    BIGINT,
   LONGITUDE    BIGINT,
   LATITUDE    BIGINT,
   COLUMN2    BIGINT,
   COLUMN3    BIGINT
   )
   STORED AS carbondata
   TBLPROPERTIES ('SPATIAL_INDEX.mygeohash.type'='geohash','SPATIAL_INDEX.mygeohash.sourcecolumns'='longitude, latitude','SPATIAL_INDEX.mygeohash.originLatitude'='39.850713','SPATIAL_INDEX.mygeohash.gridSize'='50','SPATIAL_INDEX.mygeohash.minLongitude'='115.828503','SPATIAL_INDEX.mygeohash.maxLongitude'='720.000000','SPATIAL_INDEX.mygeohash.minLatitude'='39.850713','SPATIAL_INDEX.mygeohash.maxLatitude'='720.000000','SPATIAL_INDEX'='mygeohash','SPATIAL_INDEX.mygeohash.conversionRatio'='1000000','SORT_COLUMNS'='column1,column2,column3,latitude,longitude');

Introduction to Spatial Indexes
-------------------------------

Spatial data includes multidimensional points, lines, rectangles, cubes, polygons, and other geometric objects. A spatial data object occupies a certain region of space, called spatial scope, characterized by its location and boundary. The spatial data can be either point data or region data.

-  Point data: A point has a spatial extent characterized completely by its location. It does not occupy space and has no associated boundary. Point data consists of a collection of points in a two-dimensional space. Points can be stored as a pair of longitude and latitude.
-  Region data: A region has a spatial extent with a location, and boundary. The location can be considered as the position of a fixed point in the region, such as its centroid. In two dimensions, the boundary can be visualized as a line (for finite regions, a closed loop). Region data contains a collection of regions.

Currently, only point data is supported, and it can be stored.

Longitude and latitude can be encoded as a unique GeoID. Geohash is a public-domain geocoding system invented by Gustavo Niemeyer. It encodes geographical locations into a short string of letters and digits. It is a hierarchical spatial data structure which subdivides the space into buckets of grid shape, which is one of the many applications of what is known as the Z-order curve, and generally the space-filling curve.

The Z value of a point in multiple dimensions is calculated by interleaving the binary representation of its coordinate value, as shown in the following figure. When Geohash is used to create a GeoID, data is sorted by GeoID instead of longitude and latitude. Data is stored by spatial proximity.

|image1|

Creating a Table
----------------

**GeoHash encoding**:

.. code-block::

   create table IF NOT EXISTS carbonTable
   (
   ...
   `LONGITUDE`     BIGINT,
   `LATITUDE`      BIGINT,
   ...
   )
   STORED AS carbondata
   TBLPROPERTIES ('SPATIAL_INDEX.mygeohash.type'='geohash','SPATIAL_INDEX.mygeohash.sourcecolumns'='longitude, latitude','SPATIAL_INDEX.mygeohash.originLatitude'='xx.xxxxxx','SPATIAL_INDEX.mygeohash.gridSize'='xx','SPATIAL_INDEX.mygeohash.minLongitude'='xxx.xxxxxx','SPATIAL_INDEX.mygeohash.maxLongitude'='xxx.xxxxxx','SPATIAL_INDEX.mygeohash.minLatitude'='xx.xxxxxx','SPATIAL_INDEX.mygeohash.maxLatitude'='xxx.xxxxxx','SPATIAL_INDEX'='mygeohash','SPATIAL_INDEX.mygeohash.conversionRatio'='1000000','SORT_COLUMNS'='column1,column2,column3,latitude,longitude');

**SPATIAL_INDEX** is a user-defined index handler. This handler allows users to create new columns from the table-structure column set. The new column name is the same as that of the handler name. The **type** and **sourcecolumns** properties of the handler are mandatory. Currently, the value of **type** supports only **geohash**. Carbon provides a default implementation class that can be easily used. You can extend the default implementation class to mount the customized implementation class of **geohash**. The default handler also needs to provide the following table properties:

-  **SPATIAL_INDEX.**\ *xxx*\ **.originLatitude**: specifies the origin latitude. (**Double** type.)
-  **SPATIAL_INDEX.**\ *xxx*\ **.gridSize**: specifies the grid length in meters. (**Int** type.)
-  **SPATIAL_INDEX.**\ *xxx*\ **.minLongitude**: specifies the minimum longitude. (**Double** type.)
-  **SPATIAL_INDEX.**\ *xxx*\ **.maxLongitude**: specifies the maximum longitude. (**Double** type.)
-  **SPATIAL_INDEX.**\ *xxx*\ **.minLatitude**: specifies the minimum latitude. (**Double** type.)
-  **SPATIAL_INDEX.**\ *xxx*\ **.maxLatitude**: specifies the maximum latitude. (**Double** type.)
-  **SPATIAL_INDEX.**\ *xxx*\ **.conversionRatio**: used to convert the small value of the longitude and latitude to an integer. (**Int** type.)

You can add your own table properties to the handlers in the above format and access them in your custom implementation class. **originLatitude**, **gridSize**, and **conversionRatio** are mandatory. Other parameters are optional in Carbon. You can use the **SPATIAL_INDEX.**\ *xxx*\ **.class** property to specify their implementation classes.

The default implementation class can generate handler column values for **sourcecolumns** in each row and support query based on the **sourcecolumns** filter criteria. The generated handler column is invisible to users. Except the **SORT_COLUMNS** table properties, no DDL commands or properties are allowed to contain the handler column.

.. note::

   -  By default, the generated handler column is regarded as the sorting column. If **SORT_COLUMNS** does not contain any **sourcecolumns**, add the handler column to the end of the existing **SORT_COLUMNS**. If the handler column has been specified in **SORT_COLUMNS**, its order in **SORT_COLUMNS** remains unchanged.
   -  If **SORT_COLUMNS** contains any **sourcecolumns** but does not contain the handler column, the handler column is automatically inserted before **sourcecolumns** in **SORT_COLUMNS**.
   -  If **SORT_COLUMNS** needs to contain any **sourcecolumns**, ensure that the handler column is listed before the **sourcecolumns** so that the handler column can take effect during sorting.

**GeoSOT encoding**:

.. code-block::

   CREATE TABLE carbontable(
   ...
   longitude DOUBLE,
   latitude DOUBLE,
   ...)
   STORED AS carbondata
   TBLPROPERTIES ('SPATIAL_INDEX'='xxx',
   'SPATIAL_INDEX.xxx.type'='geosot',
   'SPATIAL_INDEX.xxx.sourcecolumns'='longitude, latitude',
   'SPATIAL_INDEX.xxx.level'='21',
   'SPATIAL_INDEX.xxx.class'='org.apache.carbondata.geo.GeoSOTIndex')

.. table:: **Table 1** Parameter description

   +---------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                       | Description                                                                                                                                                                             |
   +=================================+=========================================================================================================================================================================================+
   | SPATIAL_INDEX                   | Specifies the spatial index. Its value is the same as the column name.                                                                                                                  |
   +---------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | SPATIAL_INDEX.xxx.type          | (Mandatory) The value is set to **geosot**.                                                                                                                                             |
   +---------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | SPATIAL_INDEX.xxx.sourcecolumns | (Mandatory) Specifies the source columns for calculating the spatial index. The value must be two existing columns of the double type.                                                  |
   +---------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | SPATIAL_INDEX.xxx.level         | (Optional) Specifies the columns for calculating the spatial index. The default value is **17**, through which you can obtain an accurate result and improve the computing performance. |
   +---------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | SPATIAL_INDEX.xxx.class         | (Optional) Specifies the implementation class of GeoSOT. The default value is **org.apache.carbondata.geo.GeoSOTIndex**.                                                                |
   +---------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Example:

.. code-block::

   create table geosot(
   timevalue bigint,
   longitude double,
   latitude double)
   stored as carbondata
   TBLPROPERTIES ('SPATIAL_INDEX'='mygeosot',
   'SPATIAL_INDEX.mygeosot.type'='geosot',
   'SPATIAL_INDEX.mygeosot.level'='21', 'SPATIAL_INDEX.mygeosot.sourcecolumns'='longitude, latitude');

.. _mrs_01_1451__section106234720257:

Preparing Data
--------------

-  Data file 1: **geosotdata.csv**

   .. code-block::

      timevalue,longitude,latitude
      1575428400000,116.285807,40.084087
      1575428400000,116.372142,40.129503
      1575428400000,116.187332,39.979316
      1575428400000,116.337069,39.951887
      1575428400000,116.359102,40.154684
      1575428400000,116.736367,39.970323
      1575428400000,116.720179,40.009893
      1575428400000,116.346961,40.13355
      1575428400000,116.302895,39.930753
      1575428400000,116.288955,39.999101
      1575428400000,116.17609,40.129953
      1575428400000,116.725575,39.981115
      1575428400000,116.266922,40.179415
      1575428400000,116.353706,40.156483
      1575428400000,116.362699,39.942444
      1575428400000,116.325378,39.963129

-  Data file 2: **geosotdata2.csv**

   .. code-block::

      timevalue,longitude,latitude
      1575428400000,120.17708,30.326882
      1575428400000,120.180685,30.326327
      1575428400000,120.184976,30.327105
      1575428400000,120.189311,30.327549
      1575428400000,120.19446,30.329698
      1575428400000,120.186965,30.329133
      1575428400000,120.177481,30.328911
      1575428400000,120.169713,30.325614
      1575428400000,120.164563,30.322243
      1575428400000,120.171558,30.319613
      1575428400000,120.176365,30.320687
      1575428400000,120.179669,30.323688
      1575428400000,120.181001,30.320761
      1575428400000,120.187094,30.32354
      1575428400000,120.193574,30.323651
      1575428400000,120.186192,30.320132
      1575428400000,120.190055,30.317464
      1575428400000,120.195376,30.318094
      1575428400000,120.160786,30.317094
      1575428400000,120.168211,30.318057
      1575428400000,120.173618,30.316612
      1575428400000,120.181001,30.317316
      1575428400000,120.185162,30.315908
      1575428400000,120.192415,30.315871
      1575428400000,120.161902,30.325614
      1575428400000,120.164306,30.328096
      1575428400000,120.197093,30.325985
      1575428400000,120.19602,30.321651
      1575428400000,120.198638,30.32354
      1575428400000,120.165421,30.314834

Importing Data
--------------

The GeoHash default implementation class extends the customized index abstract class. If the handler property is not set to a customized implementation class, the default implementation class is used. You can extend the default implementation class to mount the customized implementation class of **geohash**. The methods of the customized index abstract class are as follows:

-  **Init** method: Used to extract, verify, and store the handler property. If the operation fails, the system throws an exception and displays the error information.
-  **Generate** method: Used to generate indexes. It generates an index for each row of data.
-  **Query** method: Used to generate an index value range list for given input.

The commands for importing data are the same as those for importing common Carbon tables.

**LOAD DATA inpath '/tmp/**\ *geosotdata.csv*\ **' INTO TABLE geosot OPTIONS ('DELIMITER'= ',');**

**LOAD DATA inpath '/tmp/**\ *geosotdata2.csv*\ **' INTO TABLE geosot OPTIONS ('DELIMITER'= ',');**

.. note::

   For details about **geosotdata.csv** and **geosotdata2.csv**, see :ref:`Preparing Data <mrs_01_1451__section106234720257>`.

Aggregate Query of Irregular Spatial Sets
-----------------------------------------

**Query statements and filter UDFs**

-  Filtering data based on polygon

   **IN_POLYGON(pointList)**

   UDF input parameter

   +-----------+--------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type   | Description                                                                                                                                                                                                                                                                                    |
   +===========+========+================================================================================================================================================================================================================================================================================================+
   | pointList | String | Enter multiple points as a string. Each point is presented as **longitude latitude**. Longitude and latitude are separated by a space. Each pair of longitude and latitude is separated by a comma (,). The longitude and latitude values at the start and end of the string must be the same. |
   +-----------+--------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   UDF output parameter

   +-----------+---------+-----------------------------------------------------------+
   | Parameter | Type    | Description                                               |
   +===========+=========+===========================================================+
   | inOrNot   | Boolean | Checks whether data is in the specified **polygon_list**. |
   +-----------+---------+-----------------------------------------------------------+

   Example:

   .. code-block::

      select longitude, latitude from geosot where IN_POLYGON('116.321011 40.123503, 116.137676 39.947911, 116.560993 39.935276, 116.321011 40.123503');

-  Filtering data based on the polygon list

   **IN_POLYGON_LIST(polygonList, opType)**

   UDF input parameters

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                             |
   +=======================+=======================+=========================================================================================================================================================================================================================================================================================================================================================================================================================================+
   | polygonList           | String                | Inputs multiple polygons as a string. Each polygon is presented as **POLYGON ((longitude1 latitude1, longitude2 latitude2, …))**. Note that there is a space after **POLYGON**. Longitudes and latitudes are separated by spaces. Each pair of longitude and latitude is separated by a comma (,). The longitudes and latitudes at the start and end of a polygon must be the same. **IN_POLYGON_LIST** requires at least two polygons. |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |                       |                       | Example:                                                                                                                                                                                                                                                                                                                                                                                                                                |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |                       |                       | .. code-block::                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |                       |                       |    POLYGON ((116.137676 40.163503, 116.137676 39.935276, 116.560993 39.935276, 116.137676 40.163503))                                                                                                                                                                                                                                                                                                                                   |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | opType                | String                | Performs union, intersection, and subtraction on multiple polygons.                                                                                                                                                                                                                                                                                                                                                                     |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |                       |                       | Currently, the following operation types are supported:                                                                                                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |                       |                       | -  OR: A U B U C (Assume that three polygons A, B, and C are input.)                                                                                                                                                                                                                                                                                                                                                                    |
   |                       |                       | -  AND: A ∩ B ∩ C                                                                                                                                                                                                                                                                                                                                                                                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   UDF output parameter

   +-----------+---------+-----------------------------------------------------------+
   | Parameter | Type    | Description                                               |
   +===========+=========+===========================================================+
   | inOrNot   | Boolean | Checks whether data is in the specified **polygon_list**. |
   +-----------+---------+-----------------------------------------------------------+

   Example:

   .. code-block::

      select longitude, latitude from geosot where IN_POLYGON_LIST('POLYGON ((120.176433 30.327431,120.171283 30.322245,120.181411 30.314540, 120.190509 30.321653,120.185188 30.329358,120.176433 30.327431)), POLYGON ((120.191603 30.328946,120.184179 30.327465,120.181819 30.321464, 120.190359 30.315388,120.199242 30.324464,120.191603 30.328946))', 'OR');

-  Filtering data based on the polyline list

   **IN_POLYLINE_LIST(polylineList, bufferInMeter)**

   UDF input parameters

   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                                                                                                              |
   +=======================+=======================+==========================================================================================================================================================================================================================================================================================================+
   | polylineList          | String                | Inputs multiple polylines as a string. Each polyline is presented as **LINESTRING (longitude1 latitude1, longitude2 latitude2, …)**. Note that there is a space after **LINESTRING**. Longitudes and latitudes are separated by spaces. Each pair of longitude and latitude is separated by a comma (,). |
   |                       |                       |                                                                                                                                                                                                                                                                                                          |
   |                       |                       | A union will be output based on the data in multiple polylines.                                                                                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                                                                                                                          |
   |                       |                       | Example:                                                                                                                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                                                                                                          |
   |                       |                       | .. code-block::                                                                                                                                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                                                                                                                          |
   |                       |                       |    LINESTRING (116.137676 40.163503, 116.137676 39.935276, 116.260993 39.935276)                                                                                                                                                                                                                         |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | bufferInMeter         | Float                 | Polyline buffer distance, in meters. Right angles are used at the end to create a buffer.                                                                                                                                                                                                                |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   UDF output parameter

   +-----------+---------+------------------------------------------------------------+
   | Parameter | Type    | Description                                                |
   +===========+=========+============================================================+
   | inOrNot   | Boolean | Checks whether data is in the specified **polyline_list**. |
   +-----------+---------+------------------------------------------------------------+

   Example:

   .. code-block::

      select longitude, latitude from geosot where IN_POLYLINE_LIST('LINESTRING (120.184179 30.327465, 120.191603 30.328946, 120.199242 30.324464, 120.190359 30.315388)', 65);

-  Filtering data based on the GeoID range list

   **IN_POLYGON_RANGE_LIST(polygonRangeList, opType)**

   UDF input parameters

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                                                                                                          |
   +=======================+=======================+======================================================================================================================================================================================================================================================================================================+
   | polygonRangeList      | String                | Inputs multiple rangeLists as a string. Each rangeList is presented as **RANGELIST (startGeoId1 endGeoId1, startGeoId2 endGeoId2, …)**. Note that there is a space after **RANGELIST**. Start GeoIDs and end GeoIDs are separated by spaces. Each group of GeoID ranges is separated by a comma (,). |
   |                       |                       |                                                                                                                                                                                                                                                                                                      |
   |                       |                       | Example:                                                                                                                                                                                                                                                                                             |
   |                       |                       |                                                                                                                                                                                                                                                                                                      |
   |                       |                       | .. code-block::                                                                                                                                                                                                                                                                                      |
   |                       |                       |                                                                                                                                                                                                                                                                                                      |
   |                       |                       |    RANGELIST (855279368848 855279368850, 855280799610 855280799612, 855282156300 855282157400)                                                                                                                                                                                                       |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | opType                | String                | Performs union, intersection, and subtraction on multiple rangeLists.                                                                                                                                                                                                                                |
   |                       |                       |                                                                                                                                                                                                                                                                                                      |
   |                       |                       | Currently, the following operation types are supported:                                                                                                                                                                                                                                              |
   |                       |                       |                                                                                                                                                                                                                                                                                                      |
   |                       |                       | -  OR: A U B U C (Assume that three rangeLists A, B, and C are input.)                                                                                                                                                                                                                               |
   |                       |                       | -  AND: A ∩ B ∩ C                                                                                                                                                                                                                                                                                    |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   UDF output parameter

   +-----------+---------+-------------------------------------------------------------+
   | Parameter | Type    | Description                                                 |
   +===========+=========+=============================================================+
   | inOrNot   | Boolean | Checks whether data is in the specified **polyRange_list**. |
   +-----------+---------+-------------------------------------------------------------+

   Example:

   .. code-block::

      select mygeosot, longitude, latitude from geosot where IN_POLYGON_RANGE_LIST('RANGELIST (526549722865860608 526549722865860618, 532555655580483584 532555655580483594)', 'OR');

-  Performing polygon query

   **IN_POLYGON_JOIN(GEO_HASH_INDEX_COLUMN, POLYGON_COLUMN)**

   Perform join query on two tables. One is a spatial data table containing the longitude, latitude, and GeoHashIndex columns, and the other is a dimension table that saves polygon data.

   During query, **IN_POLYGON_JOIN UDF**, **GEO_HASH_INDEX_COLUMN**, and **POLYGON_COLUMN** of the polygon table are used. **Polygon_column** specifies the column containing multiple points (longitude and latitude pairs). The first and last points in each row of the Polygon table must be the same. All points in each row form a closed geometric shape.

   UDF input parameters

   +-----------------------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type   | Description                                                                                                                                                                     |
   +=======================+========+=================================================================================================================================================================================+
   | GEO_HASH_INDEX_COLUMN | Long   | GeoHashIndex column of the spatial data table.                                                                                                                                  |
   +-----------------------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | POLYGON_COLUMN        | String | Polygon column of the polygon table, the value of which is represented by the string of polygon, for example, **POLYGON (( longitude1 latitude1, longitude2 latitude2, ...))**. |
   +-----------------------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   Example:

   .. code-block::

      CREATE TABLE polygonTable(
      polygon string,
      poiType string,
      poiId String)
      STORED AS carbondata;

      insert into polygonTable select 'POLYGON ((120.176433 30.327431,120.171283 30.322245, 120.181411 30.314540,120.190509 30.321653,120.185188 30.329358,120.176433 30.327431))','abc','1';

      insert into polygonTable select 'POLYGON ((120.191603 30.328946,120.184179 30.327465, 120.181819 30.321464,120.190359 30.315388,120.199242 30.324464,120.191603 30.328946))','abc','2';

      select t1.longitude,t1.latitude from geosot t1
      inner join
      (select polygon,poiId from polygonTable where poitype='abc') t2
      on in_polygon_join(t1.mygeosot,t2.polygon) group by t1.longitude,t1.latitude;

-  Performing range_list query

   **IN_POLYGON_JOIN_RANGE_LIST(GEO_HASH_INDEX_COLUMN, POLYGON_COLUMN)**

   Use the **IN_POLYGON_JOIN_RANGE_LIST** UDF to associate the spatial data table with the polygon dimension table based on **Polygon_RangeList**. By using a range list, you can skip the conversion between a polygon and a range list.

   UDF input parameters

   +-----------------------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type   | Description                                                                                                                                                                          |
   +=======================+========+======================================================================================================================================================================================+
   | GEO_HASH_INDEX_COLUMN | Long   | GeoHashIndex column of the spatial data table.                                                                                                                                       |
   +-----------------------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | POLYGON_COLUMN        | String | Rangelist column of the Polygon table, the value of which is represented by the string of rangeList, for example, **RANGELIST (startGeoId1 endGeoId1, startGeoId2 endGeoId2, ...)**. |
   +-----------------------+--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   Example:

   .. code-block::

      CREATE TABLE polygonTable(
      polygon string,
      poiType string,
      poiId String)
      STORED AS carbondata;

      insert into polygonTable select 'RANGELIST (526546455897309184 526546455897309284, 526549831217315840 526549831217315850, 532555655580483534 532555655580483584)','xyz','2';

      select t1.*
      from geosot t1
      inner join
      (select polygon,poiId from polygonTable where poitype='xyz') t2
      on in_polygon_join_range_list(t1.mygeosot,t2.polygon);

**UDFs of spacial index tools**

-  Obtaining row number and column number of a grid converted from GeoID

   **GeoIdToGridXy(geoId)**

   UDF input parameter

   +-----------+------+-------------------------------------------------------------------------+
   | Parameter | Type | Description                                                             |
   +===========+======+=========================================================================+
   | geoId     | Long | Calculates the row number and column number of the grid based on GeoID. |
   +-----------+------+-------------------------------------------------------------------------+

   UDF output parameter

   +-----------+------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type       | Description                                                                                                                                                      |
   +===========+============+==================================================================================================================================================================+
   | gridArray | Array[Int] | Returns the grid row and column numbers contained in GeoID in array. The first digit indicates the row number, and the second digit indicates the column number. |
   +-----------+------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   Example:

   .. code-block::

      select longitude, latitude, mygeohash, GeoIdToGridXy(mygeohash) as GridXY from geoTable;

-  Converting longitude and latitude to GeoID

   **LatLngToGeoId(latitude, longitude oriLatitude, gridSize)**

   UDF input parameters

   +-------------+--------+------------------------------------------------------------+
   | Parameter   | Type   | Description                                                |
   +=============+========+============================================================+
   | longitude   | Long   | Longitude. Note: The value is an integer after conversion. |
   +-------------+--------+------------------------------------------------------------+
   | latitude    | Long   | Latitude. Note: The value is an integer after conversion.  |
   +-------------+--------+------------------------------------------------------------+
   | oriLatitude | Double | Origin latitude, required for calculating GeoID.           |
   +-------------+--------+------------------------------------------------------------+
   | gridSize    | Int    | Grid size, required for calculating GeoID.                 |
   +-------------+--------+------------------------------------------------------------+

   UDF output parameter

   +-----------+------+--------------------------------------------------------------------------+
   | Parameter | Type | Description                                                              |
   +===========+======+==========================================================================+
   | geoId     | Long | Returns a number that indicates the longitude and latitude after coding. |
   +-----------+------+--------------------------------------------------------------------------+

   Example:

   .. code-block::

      select longitude, latitude, mygeohash, LatLngToGeoId(latitude, longitude, 39.832277, 50) as geoId from geoTable;

-  Converting GeoID to longitude and latitude

   **GeoIdToLatLng(geoId, oriLatitude, gridSize)**

   UDF input parameters

   +-------------+--------+-----------------------------------------------------------------------+
   | Parameter   | Type   | Description                                                           |
   +=============+========+=======================================================================+
   | geoId       | Long   | Calculates the longitude and latitude based on GeoID.                 |
   +-------------+--------+-----------------------------------------------------------------------+
   | oriLatitude | Double | Origin latitude, required for calculating the longitude and latitude. |
   +-------------+--------+-----------------------------------------------------------------------+
   | gridSize    | Int    | Grid size, required for calculating the longitude and latitude.       |
   +-------------+--------+-----------------------------------------------------------------------+

   .. note::

      GeoID is generated based on the grid coordinates, which are the grid center. Therefore, the calculated longitude and latitude are the longitude and latitude of the grid center. There may be an error ranging from 0 degree to half of the grid size between the calculated longitude and latitude and the longitude and latitude of the generated GeoID.

   UDF output parameter

   +----------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter            | Type          | Description                                                                                                                                                                                |
   +======================+===============+============================================================================================================================================================================================+
   | latitudeAndLongitude | Array[Double] | Returns the longitude and latitude coordinates of the grid center that represent the GeoID in array. The first digit indicates the latitude, and the second digit indicates the longitude. |
   +----------------------+---------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   Example:

   .. code-block::

      select longitude, latitude, mygeohash, GeoIdToLatLng(mygeohash, 39.832277, 50) as LatitudeAndLongitude from geoTable;

-  Calculating the upper-layer GeoID of the pyramid model

   **ToUpperLayerGeoId(geoId)**

   UDF input parameter

   +-----------+------+---------------------------------------------------------------------------------+
   | Parameter | Type | Description                                                                     |
   +===========+======+=================================================================================+
   | geoId     | Long | Calculates the upper-layer GeoID of the pyramid model based on the input GeoID. |
   +-----------+------+---------------------------------------------------------------------------------+

   UDF output parameter

   ========= ==== ===================================================
   Parameter Type Description
   ========= ==== ===================================================
   geoId     Long Returns the upper-layer GeoID of the pyramid model.
   ========= ==== ===================================================

   Example:

   .. code-block::

      select longitude, latitude, mygeohash, ToUpperLayerGeoId(mygeohash) as upperLayerGeoId from geoTable;

-  Obtaining the GeoID range list using the input polygon

   **ToRangeList(polygon, oriLatitude, gridSize)**

   UDF input parameters

   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                         |
   +=======================+=======================+=====================================================================================================================================================================================+
   | polygon               | String                | Input polygon string, which is a pair of longitude and latitude.                                                                                                                    |
   |                       |                       |                                                                                                                                                                                     |
   |                       |                       | Longitude and latitude are separated by a space. Each pair of longitude and latitude is separated by a comma (,). The longitude and latitude at the start and end must be the same. |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | oriLatitude           | Double                | Origin latitude, required for calculating GeoID.                                                                                                                                    |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | gridSize              | Int                   | Grid size, required for calculating GeoID.                                                                                                                                          |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   UDF output parameter

   ========= =================== =========================================
   Parameter Type                Description
   ========= =================== =========================================
   geoIdList Buffer[Array[Long]] Converts polygons into GeoID range lists.
   ========= =================== =========================================

   Example:

   .. code-block::

      select ToRangeList('116.321011 40.123503, 116.137676 39.947911, 116.560993 39.935276, 116.321011 40.123503', 39.832277, 50) as rangeList from geoTable;

-  Calculating the upper-layer longitude of the pyramid model

   **ToUpperLongitude (longitude, gridSize, oriLat)**

   UDF input parameters

   =========== ====== ====================================================
   Parameter   Type   Description
   =========== ====== ====================================================
   longitude   Long   Input longitude, which is a long integer.
   gridSize    Int    Grid size, required for calculating longitude.
   oriLatitude Double Origin latitude, required for calculating longitude.
   =========== ====== ====================================================

   UDF output parameter

   ========= ==== ==================================
   Parameter Type Description
   ========= ==== ==================================
   longitude Long Returns the upper-layer longitude.
   ========= ==== ==================================

   Example:

   .. code-block::

      select ToUpperLongitude (-23575161504L, 50, 39.832277) as upperLongitude from geoTable;

-  Calculating the upper-layer latitude of the pyramid model

   **ToUpperLatitude(Latitude, gridSize, oriLat)**

   UDF input parameters

   =========== ====== ===================================================
   Parameter   Type   Description
   =========== ====== ===================================================
   latitude    Long   Input latitude, which is a long integer.
   gridSize    Int    Grid size, required for calculating latitude.
   oriLatitude Double Origin latitude, required for calculating latitude.
   =========== ====== ===================================================

   UDF output parameter

   ========= ==== =================================
   Parameter Type Description
   ========= ==== =================================
   Latitude  Long Returns the upper-layer latitude.
   ========= ==== =================================

   Example:

   .. code-block::

      select ToUpperLatitude (-23575161504L, 50, 39.832277) as upperLatitude from geoTable;

-  Converting longitude and latitude to GeoSOT

   **LatLngToGridCode(latitude, longitude, level)**

   UDF input parameters

   ========= ====== ==================================
   Parameter Type   Description
   ========= ====== ==================================
   latitude  Double Latitude.
   longitude Double Longitude.
   level     Int    Level. The value range is [0, 32].
   ========= ====== ==================================

   UDF output parameter

   +-----------+------+---------------------------------------------------------------------------+
   | Parameter | Type | Description                                                               |
   +===========+======+===========================================================================+
   | geoId     | Long | A number that indicates the longitude and latitude after GeoSOT encoding. |
   +-----------+------+---------------------------------------------------------------------------+

   Example:

   .. code-block::

      select LatLngToGridCode(39.930753, 116.302895, 21) as geoId;

.. |image1| image:: /_static/images/en-us_image_0000001296090372.png
