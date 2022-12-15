:original_name: mrs_03_1207.html

.. _mrs_03_1207:

How Do I Do If Error Message "requestId=4971883851071737250" Is Displayed When a Spark Job Accesses OBS?
========================================================================================================

Symptom
-------

Error message "requestId=4971883851071737250" is displayed when a Spark job accesses OBS.

Solution
--------

Log in to the node where the Spark client is located, go to the **conf** directory, and change the value of the **fs.obs.metrics.switch** parameter in the **core-site.xml** configuration file to **false**.
