:original_name: mrs_01_24089.html

.. _mrs_01_24089:

Cleaning
========

Cleaning is used to delete data of versions that are no longer required.

Hudi uses the cleaner working in the background to continuously delete unnecessary data of old versions. You can configure **hoodie.cleaner.policy** and **hoodie.cleaner.commits.retained** to use different cleaning policies and determine the number of saved commits.

You can use either of the following methods to perform cleaning:

-  Using Hudi CLI

   **cleans run --sparkMaster yarn --hoodieConfigs 'hoodie.cleaner.policy=KEEP_LATEST_COMMITS,hoodie.cleaner.commits.retained=1,hoodie.cleaner.incremental.mode=false,hoodie.keep.max.commits=3,hoodie.keep.min.commits=2**'

-  Using APIs

   **spark-submit --master yarn --jars /opt/client/Hudi/hudi/lib/hudi-client-common-**\ *xxx*\ **.jar --class org.apache.hudi.utilities.HoodieCleaner /opt/client/Hudi/hudi/lib/hudi-utilities\_**\ *xxx*\ **.jar --target-base-path /tmp/default/tb_test_mor**

For details about more cleaning parameters, see :ref:`Hudi Configuration Reference <mrs_01_24032>`.
