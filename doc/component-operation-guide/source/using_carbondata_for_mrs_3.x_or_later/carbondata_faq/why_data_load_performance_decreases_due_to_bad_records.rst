:original_name: mrs_01_1463.html

.. _mrs_01_1463:

Why Data Load Performance Decreases due to Bad Records?
=======================================================

Question
--------

Why data load performance decreases due to bad records?

Answer
------

If bad records are present in the data and **BAD_RECORDS_LOGGER_ENABLE** is **true** or **BAD_RECORDS_ACTION** is **redirect** then load performance will decrease due to extra I/O for writing failure reason in log file or redirecting the records to raw CSV.
