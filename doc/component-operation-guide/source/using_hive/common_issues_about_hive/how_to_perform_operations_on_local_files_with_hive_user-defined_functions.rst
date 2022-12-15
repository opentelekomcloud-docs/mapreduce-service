:original_name: mrs_01_1755.html

.. _mrs_01_1755:

How to Perform Operations on Local Files with Hive User-Defined Functions
=========================================================================

Question
--------

How to perform operations on local files (such as reading the content of a file) with Hive user-defined functions?

Answer
------

By default, you can perform operations on local files with their relative paths in UDF. The following are sample codes:

.. code-block::

   public String evaluate(String text) {
     // some logic
     File file = new File("foo.txt");
     // some logic
     // do return here
   }

In Hive, upload the file **foo.txt** used in UDF to HDFS, such as **hdfs://hacluster/tmp/foo.txt**. You can perform operations on the **foo.txt** file by creating UDF with the following sentences:

**create function testFunc as 'some.class' using jar 'hdfs://hacluster/somejar.jar', file 'hdfs://hacluster/tmp/foo.txt';**

In abnormal cases, if the value of **hive.fetch.task.conversion** is **more**, you can perform operations on local files in UDF by using absolute path instead of relative path. In addition, you must ensure that the file exists on all HiveServer nodes and NodeManager nodes and **omm** user have corresponding operation rights.
