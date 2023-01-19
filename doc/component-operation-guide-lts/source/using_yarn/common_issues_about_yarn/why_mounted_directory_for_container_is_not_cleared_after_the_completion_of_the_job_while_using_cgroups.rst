:original_name: mrs_01_2078.html

.. _mrs_01_2078:

Why Mounted Directory for Container is Not Cleared After the Completion of the Job While Using CGroups?
=======================================================================================================

Question
--------

Why mounted directory for Container is not cleared after the completion of the job while using CGroups?

Answer
------

The mounted path for the Container should be cleared even if job is failed.

This happens due to the deletion timeout. Some task takes more time to complete than the deletion time.

To avoid this scenario, you can go to the **All Configurations** page of Yarn by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`. Search for the **yarn.nodemanager.linux-container-executor.cgroups.delete-timeout-ms** configuration item in the search box to change the deletion interval. The value is in milliseconds.
