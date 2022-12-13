:original_name: mrs_01_1793.html

.. _mrs_01_1793:

How Do I Set the Task Priority When Submitting a MapReduce Task?
================================================================

Question
--------

How do I set the job priority when submitting a MapReduce task?

Answer
------

You can add the parameter **-Dmapreduce.job.priority=<priority>** in the command to set task priority when submitting MapReduce tasks on the client. The format is as follows:

**yarn jar** *<jar> [mainClass]* **-Dmapreduce.job.priority=**\ *\ <priority> [path1] [path2]*

The parameters in the command are described as follows:

-  *<jar>*: specifies the name of the JAR package to be run.
-  *[mainClass]*: specifies the **main** method of the class for an application project in a JAR file.
-  *<priority>*: specifies the priority of a task. The value can be **VERY_HIGH**, **HIGH**, **NORMAL**, **LOW**, or **VERY_LOW**.

-  *[path1]*: specifies the data input path.
-  *[path2]*: specifies the data output path.

For example, set the **/opt/client/HDFS/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples*.jar** package to a high-priority task.

**yarn jar /opt/client/HDFS/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples*.jar wordcount -Dmapreduce.job.priority=VERY_HIGH /DATA.txt /out/**
