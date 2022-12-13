:original_name: mrs_03_1205.html

.. _mrs_03_1205:

How Do I Do If Error Message "java.io.IOException: Connection reset by peer" Is Displayed During the Execution of a Spark Job?
==============================================================================================================================

Symptom
-------

The Spark job keeps running and error message "java.io.IOException: Connection reset by peer" is displayed.

Solution
--------

Add the **executor.memory Overhead** parameter to the parameters for submitting a job.
