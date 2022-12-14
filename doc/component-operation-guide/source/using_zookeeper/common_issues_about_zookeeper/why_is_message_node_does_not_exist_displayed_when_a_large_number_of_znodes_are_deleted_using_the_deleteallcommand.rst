:original_name: mrs_01_2114.html

.. _mrs_01_2114:

Why Is Message "Node does not exist" Displayed when A Large Number of Znodes Are Deleted Using the **deleteall** Command
========================================================================================================================

Question
--------

When the client connects to a non-leader instance, run the **deleteall** command to delete a large number of znodes, the error message "Node does not exist" is displayed, but run the **stat** command, the node status can be obtained.

Answer
------

The leader and follower data is not synchronized due to network problems or large data volume. To solve this problem, connect the client to the leader instance and delete the instance. To delete the leader node, view the IP address of the node where the leader resides by referring to :ref:`How Do I Check Which ZooKeeper Instance Is a Leader? <mrs_01_2111>`, run the **zkCli.sh -server leader** *node IP address* **2181** command to connect to the client, and then run the **deleteall** command to delete the leader node. For details, see :ref:`Using a ZooKeeper Client <mrs_01_2095>`.
