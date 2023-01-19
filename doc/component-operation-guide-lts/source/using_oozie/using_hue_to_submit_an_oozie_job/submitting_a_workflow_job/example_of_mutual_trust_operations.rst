:original_name: mrs_01_1830.html

.. _mrs_01_1830:

Example of Mutual Trust Operations
==================================

Scenario
--------

This section guides you to enable unidirectional password-free mutual trust when Oozie nodes are used to execute shell scripts of external nodes through SSH jobs.

Prerequisites
-------------

You have installed Oozie, and it can communicate with external nodes (nodes connected using SSH).

Procedure
---------

#. Ensure that the user used for SSH connection exists on the external node, and the user directory **~/.ssh** exists.

#. .. _mrs_01_1830__en-us_topic_0000001219351137_l96d21b37b10243138833bdb06d4c78ef:

   Log in to the Oozie node as user **omm** and run the **ssh-keygen -t rsa** command to generate public and private keys.

#. Run the **cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys** statement to add the public key to the **authorized_keys** file.

#. .. _mrs_01_1830__en-us_topic_0000001219351137_li19793111323111:

   Upload the **id_rsa.pub** file to an existing directory, for example, **/opt/**, on the external node as user **root**.

   **scp ~/.ssh/id_rsa.pub root@**\ *IP address of the external node*\ **:/opt/id_rsa.pub**

#. Log in to the external node where the shell is located and go to the directory described in :ref:`4 <mrs_01_1830__en-us_topic_0000001219351137_li19793111323111>`. The **id_rsa.pub** file can be found.

   Run the **cat id_rsa.pub >> ~/.ssh/authorized_keys** statement to add the public key to the **authorized_keys** file of the shell user.

#. .. _mrs_01_1830__en-us_topic_0000001219351137_la002c4226a504afaa899314ea2c1c67e:

   Change the permission on the directory.

   **chmod 700 ~/.ssh**

   **chmod 600 /opt/id_rsa.pub**

   **chmod 600 ~/.ssh/authorized_keys**

   .. note::

      -  The user of the node where shell resides (external node) has the permission to execute shell scripts and access all directories and files involved in the Shell scripts.
      -  If Oozie has multiple nodes, perform :ref:`2 <mrs_01_1830__en-us_topic_0000001219351137_l96d21b37b10243138833bdb06d4c78ef>` to :ref:`6 <mrs_01_1830__en-us_topic_0000001219351137_la002c4226a504afaa899314ea2c1c67e>` on all Oozie nodes.
