:original_name: mrs_01_1846.html

.. _mrs_01_1846:

Oozie Scheduled Tasks Are Not Executed on Time
==============================================

Question
--------

Why are not Coordinator scheduled jobs executed on time on the Hue or Oozie client?

Answer
------

Use UTC time. For example, set **start=2016-12-20T09:00Z** in **job.properties** file.
