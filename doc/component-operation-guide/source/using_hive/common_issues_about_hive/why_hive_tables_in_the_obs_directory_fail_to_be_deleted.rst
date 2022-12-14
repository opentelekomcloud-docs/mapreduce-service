:original_name: mrs_01_24486.html

.. _mrs_01_24486:

Why Hive Tables in the OBS Directory Fail to Be Deleted?
========================================================

Question
--------

In the scenario where the fine-grained permission is configured for multiple MRS users to access OBS, after the permission for deleting Hive tables in the OBS directory is added to the custom configuration of Hive, tables are deleted on the Hive client but still exist in the OBS directory.

Answer
------

You do not have the permission to delete directories on OBS. As a result, Hive tables cannot be deleted. In this case, modify the custom IAM policy of the agency and configure Hive with the permission for deleting tables in the OBS directory.
