:original_name: mrs_08_0025.html

.. _mrs_08_0025:

Bootstrap Actions
=================

Feature Introduction
--------------------

MRS provides standard elastic big data clusters on the cloud. Nine big data components, such as Hadoop and Spark, can be installed and deployed. Currently, standard cloud big data clusters cannot meet all user requirements, for example, in the following scenarios:

-  Common operating system configurations cannot meet data processing requirements, for example, increasing the maximum number of system connections.
-  Software tools or running environments need to be installed, for example, Gradle and dependency R language package.
-  Big data component packages need to be modified based on service requirements, for example, modifying the Hadoop or Spark installation package.
-  Other big data components that are not supported by MRS need to be installed.

To meet the preceding customization requirements, you can manually perform operations on the existing and newly added nodes. The overall process is complex and error-prone. In addition, manual operations cannot be traced, and data cannot be processed immediately after creating a cluster based on your demand.

Therefore, MRS supports custom bootstrap actions that enable you to run scripts on a specified node before or after a cluster component is started. You can run bootstrap actions to install third-party software that is not supported by MRS, modify the cluster running environment, and perform other customizations. If you choose to run bootstrap actions when expanding a cluster, the bootstrap actions will be run on the newly added nodes in the same way. MRS runs the script you specify as user **root**. You can run the **su - xxx** command in the script to switch the user.

Customer Benefits
-----------------

You can use the custom bootstrap actions to flexibly and easily configure your dedicated clusters and customize software installation.
