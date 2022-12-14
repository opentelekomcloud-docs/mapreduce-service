:original_name: mrs_01_2079.html

.. _mrs_01_2079:

Why the Job Fails with HDFS_DELEGATION_TOKEN Expired Exception?
===============================================================

Question
--------

Why is the HDFS_DELEGATION_TOKEN expired exception reported when a job fails in security mode?

Answer
------

HDFS_DELEGATION_TOKEN expires because the token is not updated or it is accessed after max. lifetime.

Ensure the following parameter value of max. lifetime of the token is greater than the job running time.

**dfs.namenode.delegation.token.max-lifetime**\ =\ **604800000** (1 week by default)

Go to the **All Configurations** page of HDFS by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>` and search for this parameter in the search box.

.. note::

   You are advised to set this parameter to a value that is multiple times of the number of hours within the max. lifecycle of the token.
