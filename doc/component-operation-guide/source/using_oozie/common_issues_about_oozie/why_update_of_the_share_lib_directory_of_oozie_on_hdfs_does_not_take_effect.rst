:original_name: mrs_01_1847.html

.. _mrs_01_1847:

Why Update of the share lib Directory of Oozie on HDFS Does Not Take Effect?
============================================================================

Symptom
-------

A new JAR package is uploaded to the **/user/oozie/share/lib** directory on HDFS. However, an error indicating that the class cannot be found is reported during task execution.

Solution
--------

Run the following command on the client to refresh the directory:

**oozie admin -oozie https://xxx.xxx.xxx.xxx:21003/oozie -sharelibupdate**
