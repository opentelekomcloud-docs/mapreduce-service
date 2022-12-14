:original_name: mrs_01_2360.html

.. _mrs_01_2360:

Using HDFS AZ Mover
===================

Scenario
--------

AZ Mover is a copy migration tool used to move copies to meet the new AZ policies set on the directory. It can be used to migrate copies from one AZ policy to another. AZ Mover instructs NameNode to move copies based on a new AZ policy. If the NameNode refuses to delete the old copies, the new policy may not be met. For example, the copies are marked as outdated.

Restrictions
------------

-  Changing the policy name to **LOCAL_AZ** is the same as that to **ONE_AZ** because the client location cannot be determined when the uploaded file is written.
-  Mover cannot determine the AZ status. As a result, the copy may be moved to the abnormal AZ and depends on NameNode for further processing.
-  Mover depends on whether the number of DataNodes in each AZ meets the minimum requirement. If the AZ Mover is executed in an AZ with a small number of DataNodes, the result may be different from the expected result.
-  Mover only meets the AZ-level policies and does not guarantee to meet the basic block placement policy (BPP).
-  Mover does not support the change of replication factors. If the number of copies in the new AZ is different from that in the old AZ, an exception occurs.

Procedure
---------

#. Run the following command to go to the client installation directory.

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If the cluster is in security mode, the user must have the read permission on the source directory or file and the write permission on the destination directory, and run the following command to authenticate the user: In normal mode, skip user authentication.

   **kinit** *Component service user*

#. Create a directory and set an AZ policy.

   Run the following command to create a directory.

   **hdfs dfs -mkdir** <*path*>

   Run the following command to set the AZ policy (**azexpression** indicates the AZ policy):

   **hdfs dfsadmin -setAZExpression** *<path*\ **>** *<azexpression*>

   Run the following command to view the AZ policy:

   **hdfs dfsadmin -getAZExpression** *<path*>

#. Upload files to the directory.

   **hdfs dfs -put <**\ *localfile*\ **> <**\ *hdfs-path*\ **>**

#. Delete the old policy from the directory and set a new policy.

   Run the following command to clear the old policy:

   **hdfs dfsadmin -clearAZExpression <**\ *path*\ **>**

   Run the following command to configure a new policy:

   **hdfs dfsadmin -setAZExpression <**\ *path*\ **> <**\ *azexpression*\ **>**

#. Run the **azmover** command to make the copy distribution meet the new AZ policy.

   **hdfs azmover -p /targetDirecotry**
