:original_name: mrs_03_1215.html

.. _mrs_03_1215:

How Do I Do If a Flink Job Fails to Execute and the Error Message "java.lang.NoSuchFieldError: SECURITY_SSL_ENCRYPT_ENABLED" Is Displayed?
==========================================================================================================================================

Symptom
-------

A Flink job fails to be executed and the following error message is displayed:

.. code-block::

   Caused by: java.lang.NoSuchFieldError: SECURITY_SSL_ENCRYPT_ENABLED

Solution
--------

The third-party dependency package in the customer code conflicts with the cluster package. As a result, the job fails to be submitted to the MRS cluster. You need to modify the dependency package, set the scope of the open source Hadoop package and Flink package in the POM file to **provide**, and pack and execute the job again.
