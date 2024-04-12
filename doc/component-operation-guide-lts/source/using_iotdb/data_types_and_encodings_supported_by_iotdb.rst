:original_name: mrs_01_24764.html

.. _mrs_01_24764:

Data Types and Encodings Supported by IoTDB
===========================================

IoTDB supports the following data types and encodings. For details, see :ref:`Table 1 <mrs_01_24764__table4767452502>`.

.. _mrs_01_24764__table4767452502:

.. table:: **Table 1** Data types and encodings supported by IoTDB

   ======= ============ ===========================================
   Type    Description  Supported Encoding
   ======= ============ ===========================================
   BOOLEAN Boolean      PLAIN, RLE
   INT32   Integer      PLAIN, RLE, TS_2DIFF, GORILLA, FREQ, ZIGZAG
   INT64   Long integer PLAIN, RLE, TS_2DIFF, GORILLA, FREQ, ZIGZAG
   FLOAT   Float        PLAIN, RLE, TS_2DIFF, GORILLA, FREQ
   DOUBLE  Double       PLAIN, RLE, TS_2DIFF, GORILLA, FREQ
   TEXT    String       PLAIN, DICTIONARY
   ======= ============ ===========================================
