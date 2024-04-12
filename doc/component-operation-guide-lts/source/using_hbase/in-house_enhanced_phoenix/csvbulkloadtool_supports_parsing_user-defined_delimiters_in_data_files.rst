:original_name: mrs_01_24580.html

.. _mrs_01_24580:

CsvBulkloadTool Supports Parsing User-Defined Delimiters in Data Files
======================================================================

Scenario
--------

Phoenix provides CsvBulkloadTool, a batch data import tool. This tool supports import of user-defined delimiters. Specifically, users can use any visible characters within the specified length as delimiters to import data files.

.. note::

   This section applies only to MRS 3.2.0 or later.

Constraints
-----------

-  User-defined delimiters cannot be an empty string.
-  A user-defined delimiter can contain a maximum of 16 characters.

   .. note::

      A long delimiter affects parsing efficiency, slows down data import, reduces the proportion of valid data, and results in large files. Use short delimiters as possible.

-  User-defined delimiters must be visible characters.

   .. note::

      A user-defined delimiter whitelist can be configured to avoid any injection issues possible. Currently, the following delimiters are supported: letters, numbers, and special characters (:literal:`\`~!@#$%^&*()\\\\-_=+\\\\[\\\\]{}\\\\\\\\|;:'\\",<>./?`).

-  The start and end of a user-defined delimiter cannot be the same.

Description of New Parameters
-----------------------------

The following two parameters are added based on the open source CsvBulkloadTool:

-  **--multiple-delimiter(-md)**

   This parameter specifies the user-defined delimiter. If this parameter is specified, it takes effect preferentially and overwrites the **-d** parameter in the original command.

-  **--multiple-delimiter-skip-check(-mdsc)**

   This parameter is used to skip the delimiter length and whitelist verification. It is not recommended.

Procedure
---------

#. .. _mrs_01_24580__li1033704115320:

   Upload the data file to the node where the client is deployed. For example, upload the **data.csv** file to the **/opt/test** directory on the target node. The delimiter is **\|^[**. The file content is as follows:

   |image1|

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to go to the client directory:

   **cd** *Client installation directory*

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Run the following command to authenticate the current user if Kerberos authentication is enabled for the current cluster. The current user must have the permissions to create HBase tables and operate HDFS.

   **kinit** *Component service user*

   Run the following command to set the Hadoop username if Kerberos authentication is not enabled for the current cluster:

   **export HADOOP_USER_NAME=hbase**

#. Run the following command to upload the data file **data.csv** in :ref:`1 <mrs_01_24580__li1033704115320>` to an HDFS directory, for example, **/tmp**:

   **hdfs dfs -put /opt/test/data.csv /tmp**

#. Run the Phoenix client command.

   **sqlline.py**

#. Run the following command to create the **TEST** table:

   **CREATE TABLE TEST ( ID INTEGER NOT NULL PRIMARY KEY, NAME VARCHAR, AGE INTEGER, ADDRESS VARCHAR, GENDER BOOLEAN, A DECIMAL, B DECIMAL ) split on (1, 2, 3,4,5,6,7,8,9);**

   After the table is created, run the **!quit** command to exit the Phoenix CLI.

#. Run the following import command:

   **hbase org.apache.phoenix.mapreduce.CsvBulkLoadTool -md '**\ *User-defined delimiter*\ **' -t** *Table name* **-i** *Data path*

   For example, to import the **data.csv** file to the **TEST** table, run the following command:

   **hbase org.apache.phoenix.mapreduce.CsvBulkLoadTool -md '\|^[' -t** **TEST** **-i** **/tmp/data.csv**

#. Run the following command to view data imported to the **TEST** table:

   **sqlline.py**

   **SELECT \* FROM TEST LIMIT 10;**

   |image2|

.. |image1| image:: /_static/images/en-us_image_0000001532503042.png
.. |image2| image:: /_static/images/en-us_image_0000001583182157.png
