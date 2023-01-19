:original_name: mrs_01_0963.html

.. _mrs_01_0963:

Creating User-Defined Hive Functions
====================================

When built-in functions of Hive cannot meet requirements, you can compile user-defined functions (UDFs) and use them for query.

According to implementation methods, UDFs are classified as follows:

-  Common UDFs: used to perform operations on a single data row and export a single data row.
-  User-defined aggregating functions (UDAFs): used to input multiple data rows and export a single data row.
-  User-defined table-generating functions (UDTFs): used to perform operations on a single data row and export multiple data rows.

According to use methods, UDFs are classified as follows:

-  Temporary functions: used only in the current session and must be recreated after a session restarts.
-  Permanent functions: used in multiple sessions. You do not need to create them every time a session restarts.

.. note::

   You need to properly control the memory and thread usage of variables in UDFs. Improper control may cause memory overflow or high CPU usage.

The following uses AddDoublesUDF as an example to describe how to compile and use UDFs.

Function
--------

AddDoublesUDF is used to add two or more floating point numbers. In this example, you can learn how to write and use UDFs.

.. note::

   -  A common UDF must be inherited from **org.apache.hadoop.hive.ql.exec.UDF**.
   -  A common UDF must implement at least one **evaluate()**. The evaluate function supports overloading.
   -  To develop a customized function, you need to add the **hive-exec-3.1.0.jar** dependency package to the project. The package can be obtained from the Hive installation directory.

How to Use
----------

#. Packing programs as **AddDoublesUDF.jar** on the client node, and upload the package to a specified directory in HDFS, for example, **/user/hive_examples_jars**.

   Both the user who creates the function and the user who uses the function must have the read permission on the file.

   The following are example statements:

   **hdfs dfs -put ./hive_examples_jars /user/hive_examples_jars**

   **hdfs dfs -chmod 777 /user/hive_examples_jars**

#. Check the cluster authentication mode.

   -  In security mode, log in to the beeline client as a user with the Hive management permission and run the following commands:

      **kinit** *Hive service user*

      **beeline**

      **set role admin;**

   -  In common mode, run the following command:

      **beeline -n** *Hive service user*

#. Define the function in HiveServer. Run the following SQL statement to create a permanent function:

   **CREATE FUNCTION** *addDoubles* **AS 'com.xxx.bigdata.hive.example.udf.AddDoublesUDF' using jar 'hdfs://hacluster/user/hive_examples_jars/AddDoublesUDF.jar\ ';**

   *addDoubles* indicates the function alias that is used for SELECT query.

   Run the following statement to create a temporary function:

   **CREATE TEMPORARY FUNCTION addDoubles AS 'com.xxx.bigdata.hive.example.udf.AddDoublesUDF' using jar 'hdfs://hacluster/user/hive_examples_jars/AddDoublesUDF.jar\ ';**

   -  *addDoubles* indicates the function alias that is used for SELECT query.
   -  **TEMPORARY** indicates that the function is used only in the current session with the HiveServer.

#. Run the following SQL statement to use the function on the HiveServer:

   **SELECT addDoubles(1,2,3);**

   .. note::

      If an [Error 10011] error is displayed when you log in to the client again, run the **reload function;** command and then use this function.

#. Run the following SQL statement to delete the function from the HiveServer:

   **DROP FUNCTION addDoubles;**

Extended Applications
---------------------

None
