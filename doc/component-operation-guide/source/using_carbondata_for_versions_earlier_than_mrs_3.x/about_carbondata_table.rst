:original_name: mrs_01_0387.html

.. _mrs_01_0387:

About CarbonData Table
======================

Description
-----------

CarbonData tables are similar to tables in the relational database management system (RDBMS). RDBMS tables consist of rows and columns to store data. CarbonData tables have fixed columns and also store structured data. In CarbonData, data is saved in entity files.

Supported Data Types
--------------------

CarbonData tables support the following data types:

-  Int
-  String
-  BigInt
-  Decimal
-  Double
-  TimeStamp

:ref:`Table 1 <mrs_01_0387__te1b84a2aca034e4b9e5745ab6b7bb9fd>` describes the details about each data type.

.. _mrs_01_0387__te1b84a2aca034e4b9e5745ab6b7bb9fd:

.. table:: **Table 1** CarbonData data types

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Data Type                         | Description                                                                                                                                                          |
   +===================================+======================================================================================================================================================================+
   | Int                               | 4-byte signed integer ranging from -2,147,483,648 to 2,147,483,647                                                                                                   |
   |                                   |                                                                                                                                                                      |
   |                                   | .. note::                                                                                                                                                            |
   |                                   |                                                                                                                                                                      |
   |                                   |    If a non-dictionary column is of the **int** data type, it is internally stored as the **BigInt** type.                                                           |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | String                            | The maximum character string length is 100000.                                                                                                                       |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | BigInt                            | Data is saved using the 64-bit technology. The value ranges from -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807.                                            |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Decimal                           | The default value is (10,0) and maximum value is (38,38).                                                                                                            |
   |                                   |                                                                                                                                                                      |
   |                                   | .. note::                                                                                                                                                            |
   |                                   |                                                                                                                                                                      |
   |                                   |    When query with filters, append **BD** to the number to achieve accurate results. For example, **select \* from carbon_table where num = 1234567890123456.22BD**. |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Double                            | Data is saved using the 64-bit technology. The value ranges from 4.9E-324 to 1.7976931348623157E308.                                                                 |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | TimeStamp                         | **yyyy-MM-dd HH:mm:ss** format is used by default.                                                                                                                   |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   Measurement of all Integer data is processed and displayed using the **BigInt** data type.
