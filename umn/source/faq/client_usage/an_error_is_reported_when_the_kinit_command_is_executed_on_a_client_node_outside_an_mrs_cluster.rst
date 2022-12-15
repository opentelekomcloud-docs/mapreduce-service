:original_name: mrs_03_1251.html

.. _mrs_03_1251:

An Error Is Reported When the kinit Command Is Executed on a Client Node Outside an MRS Cluster
===============================================================================================

Symptom
-------

After the client is installed on a node outside an MRS cluster and the **kinit** command is executed, the following error information is displayed:

.. code-block::

   -bash kinit Permission denied

The following error information is displayed when the **java** command is executed:

.. code-block::

   -bash: /xxx/java: Permission denied

After running the **ll /**\ *Java installation path*\ **/JDK/jdk/bin/java** command, it is found that the file execution permission is correct.

Fault Locating
--------------

Run the **mount \| column -t** command to check the status of the mounted partition. It is found that the partition status of the mount point where the Java execution file is located is **noexec**. In the current environment, the data disk where the MRS client is installed is set to **noexec**, that is, binary file execution is prohibited. As a result, Java commands cannot be executed.

Solution
--------

#. Log in to the node where the MRS client is located as user **root**.
#. Remove the configuration item **noexec** of the data disk where the MRS client is located from the **/etc/fstab** file.
#. Run the **umount** command to detach the data disk, and then run the **mount -a** command to remount the data disk.
