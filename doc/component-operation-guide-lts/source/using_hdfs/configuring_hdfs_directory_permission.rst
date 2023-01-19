:original_name: mrs_01_0797.html

.. _mrs_01_0797:

Configuring HDFS Directory Permission
=====================================

Scenario
--------

The permission for some HDFS directories is **777** or **750** by default, which brings potential security risks. You are advised to modify the permission for the HDFS directories after the HDFS is installed to increase user security.

Procedure
---------

Log in to the HDFS client as the administrator and run the following command to modify the permission for the **/user** directory.

The permission is set to **1777**, that is, **1** is added to the original permission. This indicates that only the user who creates the directory can delete it.

**hdfs dfs -chmod 1777** */user*

To ensure security of the system file, you are advised to harden the security for non-temporary directories. The following directories are examples:

-  /user:777
-  /mr-history:777
-  /mr-history/tmp:777
-  /mr-history/done:777
-  /user/mapred:755
