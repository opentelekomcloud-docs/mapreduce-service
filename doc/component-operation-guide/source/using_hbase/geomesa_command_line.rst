:original_name: mrs_01_24119.html

.. _mrs_01_24119:

GeoMesa Command Line
====================

.. note::

   This section applies only to MRS 3.1.0 or later.

This section describes common GeoMesa commands. For more GeoMesa commands, visit https://www.geomesa.org/documentation/user/accumulo/commandline.html.

After installing the HBase client and loading environment variables, you can use the geomesa-hbase command line.

-  Viewing **classpath**

   After you run the **classpath** command, all **classpath** information of the current command line tool will be returned.

   **bin/geomesa-hbase classpath**

-  Creating a table

   Run the **create-schema** command to create a table. When creating a table, you need to specify the directory name, table name, and table specifications at least.

   **bin/geomesa-hbase create-schema -c geomesa -f test -s Who:String,What:java.lang.Long,When:Date,*Where:Point:srid=4326,Why:String**

-  Describing a table

   Run the **describe-schema** command to obtain table descriptions. When describing a table, you need to specify the directory name and table name.

   **bin/geomesa-hbase describe-schema -c geomesa -f test**

-  Importing data in batches

   Run the **ingest** command to import data in batches. When importing data, you need to specify the directory name, table name, table specifications, and the related data converter.

   The data in the **data.csv** file contains license plate number, vehicle color, longitude, latitude, and time. Save the data table to the folder.

   .. code-block::

      AAA,red,113.918417,22.505892,2017-04-09 18:03:46
      BBB,white,113.960719,22.556511,2017-04-24 07:38:47
      CCC,blue,114.088333,22.637222,2017-04-23 15:07:54
      DDD,yellow,114.195456,22.596103,2017-04-21 21:27:06
      EEE,black,113.897614,22.551331,2017-04-09 09:34:48

   Table structure definition: **myschema.sft**. Save **myschema.sft** to the **conf** folder of the GeoMesa command line tool.

   .. code-block::

      geomesa.sfts.cars = {
         attributes = [
              { name = "carid", type = "String", index = true }
              { name = "color", type = "String", index = false }
              { name = "time", type = "Date",   index = false }
              { name = "geom", type = "Point",  index = true,srid = 4326,default = true }
         ]
      }

   Converter definition: **myconvertor.convert** Save **myconvertor.convert** to the **conf** folder of the GeoMesa command line tool.

   .. code-block::

      geomesa.converters.cars= {
            type   = "delimited-text",
            format = "CSV",
            id-field = "$fid",
            fields = [
              { name = "fid",     transform = "concat($1,$5)" }
              { name = "carid",   transform = "$1::string" }
              { name = "color",   transform = "$2::string" }
              { name = "lon",     transform = "$3::double" }
              { name = "lat",     transform = "$4::double" }
              { name = "geom",    transform = "point($lon,$lat)" }
              { name = "time",    transform = "date('YYYY-MM-dd HH:mm:ss',$5)" }
            ]
      }

   Run the following command to import data:

   **bin/geomesa-hbase ingest -c geomesa -C conf/myconvertor.convert -s conf/myschema.sft data/data.csv**

   For details about other parameters for importing data, visit https://www.geomesa.org/documentation/user/accumulo/examples.html#ingesting-data.

-  Querying explanations

   Run the **explain** command to obtain execution plan explanations of the specified query statement. You need to specify the directory name, table name, and query statement.

   **bin/geomesa-hbase explain -c geomesa -f cars -q "carid = 'BBB'"**

-  Analyzing statistics

   Run the **stats-analyze** command to conduct statistical analysis on the data table. In addition, you can run the **stats-bounds**, **stats-count**, **stats-histogram**, and **stats-top-k** commands to collect more detailed statistics on the data table.

   **bin/geomesa-hbase stats-analyze -c geomesa -f cars**

   **bin/geomesa-hbase stats-bounds -c geomesa -f cars**

   **bin/geomesa-hbase stats-count -c geomesa -f cars**

   **bin/geomesa-hbase stats-histogram -c geomesa -f cars**

   **bin/geomesa-hbase stats-top-k -c geomesa -f cars**

-  Exporting a feature

   Run the **export** command to export a feature. When exporting the feature, you must specify the directory name and table name. In addition, you can specify a query statement to export the feature.

   **bin/geomesa-hbase export -c geomesa -f cars -q "carid = 'BBB'"**

-  Deleting a feature

   Run the **delete-features** command to delete a feature. When deleting the feature, you must specify the directory name and table name. In addition, you can specify a query statement to delete the feature.

   **bin/geomesa-hbase delete-features -c geomesa -f cars -q "carid = 'BBB'"**

-  Obtain the names of all tables in the directory.

   Run the **get-type-names** command to obtain the names of tables in the specified directory.

   **bin/geomesa-hbase get-type-names -c geomesa**

-  Deleting a table

   Run the **remove-schema** command to delete a table. You need to specify the directory name and table name at least.

   **bin/geomesa-hbase remove-schema -c geomesa -f test**

   **bin/geomesa-hbase remove-schema -c geomesa -f cars**

-  Deleting a catalog

   Run the **delete-catalog** command to delete the specified catalog.

   **bin/geomesa-hbase delete-catalog -c geomesa**
