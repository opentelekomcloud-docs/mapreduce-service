:original_name: mrs_01_2041.html

.. _mrs_01_2041:

Why Does the "Permission denied" Exception Occur When I Create a Temporary Table or View in Spark-beeline?
==========================================================================================================

Question
--------

In normal mode, when I create a temporary table or view in spark-beeline, the error message "Permission denied" is displayed, indicating that I have no permissions on the HDFS directory. The error log information is as follows:

.. code-block::

   org.apache.hadoop.security.AccessControlException Permission denied: user=root, access=EXECUTE, inode="/tmp/spark/sparkhive-scratch/omm/e579a76f-43ed-4014-8a54-1072c07ceeff/_tmp_space.db/52db1561-60b0-4e7d-8a25-c2eaa44850a9":omm:hadoop:drwx------

Answer
------

In normal mode, if you run the spark-beeline command as a non-omm user, **root** user for example, without specifying the **-n** parameter, your account is still the root user. After spark-beeline is started, a new HDFS directory is created by JDBCServer. In the current version of DataSight, the user that starts the JDBCServer is **omm**. In versions earlier than DataSight V100R002C30, the user is **root**. Therefore, the owner of the HDFS directory is **omm** and the group is **hadoop**. The HDFS directory is used when you create a temporary table or view in spark-beeline and the user **root** is a common user in HDFS and has no permissions on the directory of user **omm**. As a result, the "Permission denied" exception occurs.

In normal mode, only user **omm** can create a temporary table or view. To solve this problem, you can specify the **-n omm** option for user **omm** when starting spark-beeline. In this way, you have the permissions to perform operations on the HDFS directory.
