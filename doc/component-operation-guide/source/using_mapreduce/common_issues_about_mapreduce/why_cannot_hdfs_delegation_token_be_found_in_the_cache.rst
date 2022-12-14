:original_name: mrs_01_1792.html

.. _mrs_01_1792:

Why Cannot HDFS_DELEGATION_TOKEN Be Found in the Cache?
=======================================================

Question
--------

In security mode, why delegation token HDFS_DELEGATION_TOKEN is not found in the cache?

Answer
------

In MapReduce, by default HDFS_DELEGATION_TOKEN will be canceled after the job completion. So if the token has to be re- used for the next job then the token will not be found in the cache.

To re-use the same token in subsequent job set the below parameter for the MR job configuration. When it is false the user can re-sue the same token.

.. code-block::

   jobConf.setBoolean("mapreduce.job.complete.cancel.delegation.tokens", false);
