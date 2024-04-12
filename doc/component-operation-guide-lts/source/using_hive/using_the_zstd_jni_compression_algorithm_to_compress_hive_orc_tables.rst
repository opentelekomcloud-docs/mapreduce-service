:original_name: mrs_01_24507.html

.. _mrs_01_24507:

Using the ZSTD_JNI Compression Algorithm to Compress Hive ORC Tables
====================================================================

Scenario
--------

ZSTD_JNI is a native implementation of the ZSTD compression algorithm. Compared with ZSTD, ZSTD_JNI has higher compression read/write efficiency and compression ratio, and allows you to specify the compression level as well as the compression mode for data columns in a specific format.

Currently, only ORC tables can be compressed using ASTD_JNI. By contrast, ZSTD enables you to compress tables in the full storage format. Therefore, you are advised to use this feature only when you have high requirements on data compression.

.. note::

   This section applies only to MRS 3.2.0 or later.

Example
-------

#. Log in to the node where the client is installed as the Hive client installation user.

#. Run the following command to switch to the client installation directory, for example, **/opt/client**:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Check whether the cluster authentication mode is in security mode.

   -  If yes, run the following command to perform user authentication and then go to :ref:`5 <mrs_01_24507__li333142945916>`.

      **kinit** *Hive service user*

   -  If no, go to :ref:`5 <mrs_01_24507__li333142945916>`.

#. .. _mrs_01_24507__li333142945916:

   Run the following command to log in to the Hive client:

   **beeline**

#. Create a table in ZSTD_JNI compression format as follows:

   -  Run the following example command to set the **orc.compress** parameter to **ZSTD_JNI** when using this compression algorithm to create an ORC table:

      **create table tab_1(...) stored as orc TBLPROPERTIES("orc.compress"="ZSTD_JNI");**

   -  The compression level of ZSTD_JNI ranges from 1 to 19. A larger value indicates a higher compression ratio but a slower read/write speed. A smaller value indicates a lower compression ratio but a faster compression speed compared with read/write speed and the other way around. The default value is **6**. You can set the compression level through the **orc.global.compress.level** parameter, as shown in the follows.

      **create table tab_1(...) stored as orc TBLPROPERTIES("orc.compress"="ZSTD_JNI", 'orc.global.compress.level'='3');**

   -  This compression algorithm allows you to compress service data and columns in a specific data format. Currently, data in the following formats is supported: JSON data columns, Base64 data columns, timestamp data columns, and UUID data columns. You can achieve this function by setting the **orc.column.compress** parameter during table creation.

      The following example code shows how to use ZSTD_JNI to compress data in the JSON, Base64, timestamp, and UUID formats.

      **create table test_orc_zstd_jni(f1 int, f2 string, f3 string, f4 string, f5 string) stored as orc**

      **TBLPROPERTIES('orc.compress'='ZSTD_JNI', 'orc.column.compress'='[{"type":"cjson","columns":"f2"},{"type":"base64","columns":"f3"},{"type ":"gorilla","columns":{"format": "yyyy-MM-dd HH:mm:ss.SSS", "columns": "f4"}},{"type":"uuid","columns":"f5"}]');**

      You can insert data in the corresponding format based on the site requirements to further compress the data.
