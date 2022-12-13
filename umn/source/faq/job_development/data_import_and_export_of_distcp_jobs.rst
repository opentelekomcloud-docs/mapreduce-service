:original_name: mrs_03_1238.html

.. _mrs_03_1238:

Data Import and Export of DistCP Jobs
=====================================

-  Does a DistCP job compare data consistency during data import and export?

   No. DistCP jobs only copy data but do not modify it.

-  When data is exported from a DistCP job, if some files already exist in OBS, how will the job process the files?

   DistCP jobs will overwrite the files in OBS.
