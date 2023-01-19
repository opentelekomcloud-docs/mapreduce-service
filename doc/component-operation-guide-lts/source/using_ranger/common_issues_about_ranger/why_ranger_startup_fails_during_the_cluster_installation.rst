:original_name: mrs_01_1867.html

.. _mrs_01_1867:

Why Ranger Startup Fails During the Cluster Installation?
=========================================================

Problem
-------

During cluster installation, Ranger fails to be started, and the error message "ERROR: cannot drop sequence X_POLICY_REF_ACCESS_TYPE_SEQ " is displayed in the task list of the Manager process. How do I resolve this problem and properly install Ranger?

Answer
------

This issue may occur when two RangerAmdin instances are installed. If the instance installation fails, manually restart one RangerAdmin instance and then restart the other instance.
