:original_name: mrs_01_1640.html

.. _mrs_01_1640:

Operation Failures Occur in Stopping BulkLoad On the Client
===========================================================

Question
--------

Why submitted operations fail by stopping BulkLoad on the client during BulkLoad data importing?

Answer
------

When BulkLoad is enabled on the client, a partitioner file is generated and used to demarcate the range of Map task data inputting. The file is automatically deleted when BulkLoad exists on the client. In general, if all map tasks are enabled and running, the termination of BulkLoad on the client does not cause the failure of submitted operations. However, due to the retry and speculative execution mechanism of Map tasks, a Map task is performed again if failures of the Reduce task to download the data of the completed Map task exceed the limit. In this case, if BulkLoad already exists on the client, the retry Map task fails and the operation failure occurs because the partitioner file is missing. Therefore, it is recommended not to stop BulkLoad on the client during BulkLoad data importing.
