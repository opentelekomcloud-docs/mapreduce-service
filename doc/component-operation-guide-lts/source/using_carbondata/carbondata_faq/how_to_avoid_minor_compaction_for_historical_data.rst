:original_name: mrs_01_1459.html

.. _mrs_01_1459:

How to Avoid Minor Compaction for Historical Data?
==================================================

Question
--------

How to avoid minor compaction for historical data?

Answer
------

If you want to load historical data first and then the incremental data, perform following steps to avoid minor compaction of historical data:

#. Load all historical data.
#. Configure the major compaction size to a value smaller than the segment size of historical data.
#. Run the major compaction once on historical data so that these segments will not be considered later for minor compaction.
#. Load the incremental data.
#. You can configure the minor compaction threshold as required.

For example:

#. Assume that you have loaded all historical data to CarbonData and the size of each segment is 500 GB.
#. Set the threshold of major compaction property to **carbon.major.compaction.size** = **491520** (480 GB x 1024).
#. Run major compaction. All segments will be compacted because the size of each segment is more than configured size.
#. Perform incremental loading.
#. Configure the minor compaction threshold to **carbon.compaction.level.threshold** = **6,6**.
#. Run minor compaction. As a result, only incremental data is compacted.
