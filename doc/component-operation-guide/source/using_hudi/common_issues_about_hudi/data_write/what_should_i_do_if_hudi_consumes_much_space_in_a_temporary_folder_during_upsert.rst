:original_name: mrs_01_24074.html

.. _mrs_01_24074:

What Should I Do If Hudi Consumes Much Space in a Temporary Folder During Upsert?
=================================================================================

Question
--------

Hudi consumes much space in a temporary folder during upsert.

Answer
------

Hudi will spill part of input data to disk if the maximum memory for merge is reached when much input data is upserted.

If the memory is sufficient, increase the memory of the Spark executor and add the **hoodie.memory.merge.fraction** option, for example, **option("hoodie.memory.merge.fraction", "0.8")**.
