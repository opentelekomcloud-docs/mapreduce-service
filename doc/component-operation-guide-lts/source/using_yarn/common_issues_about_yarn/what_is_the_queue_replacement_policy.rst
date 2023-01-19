:original_name: mrs_01_2086.html

.. _mrs_01_2086:

What Is the Queue Replacement Policy?
=====================================

Question
--------

If a user belongs to multiple user groups with different default queue configurations, which queue will be selected as the default queue when an application is submitted?

Answer
------

In the **superior-users.xml** file, if the default queue of the user is configured, the configured default queue will be used. If the default queue of the user is not specified, the default queue of the first user group in the **superior-users.xml** file is used.
