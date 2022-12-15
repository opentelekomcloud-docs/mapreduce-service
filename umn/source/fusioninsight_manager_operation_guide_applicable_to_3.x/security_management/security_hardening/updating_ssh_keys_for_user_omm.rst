:original_name: admin_guide_000285.html

.. _admin_guide_000285:

Updating SSH Keys for User omm
==============================

Scenario
--------

During cluster installation, the system automatically generate the SSH public key and private key for user **omm** to establish the trust relationship between nodes. After the cluster is installed, if the original keys are accidentally disclosed or new keys are used, the system administrator can perform the following operations to manually change the keys.

Prerequisites
-------------

-  The cluster has been stopped.
-  No other management operations are being performed.

Procedure
---------

#. Log in as user **omm** to the node whose SSH keys need to be replaced.

   If the node is a Manager management node, run the following command on the active management node.

#. Run the following command to disable logout upon timeout:

   **TMOUT=0**

   .. note::

      After the operations in this section are complete, run the **TMOUT=**\ *Timeout interval* command to restore the timeout interval in a timely manner. For example, **TMOUT=600** indicates that a user is logged out if the user does not perform any operation within 600 seconds.

#. Run the following command to generate a key for the node:

   -  If the node is a Manager management node, run the following command:

      **sh ${CONTROLLER_HOME}/sbin/update-ssh-key.sh**

   -  If the node is a non-Manager management node, run the following command:

      **sh ${NODE_AGENT_HOME}/bin/update-ssh-key.sh**

   If "Succeed to update ssh private key." is displayed when the preceding command is executed, the SSH key is generated successfully.

4.  Run the following command to copy the public key of the node to the active management node:

    **scp ${HOME}/.ssh/id_rsa.pub** *oms_ip*\ **:${HOME}/.ssh/id_rsa.pub_bak**

    *oms_ip*: indicates the IP address of the active management node.

    Enter the password of user **omm** to copy the files.

5.  Log in to the active management node as user **omm**.

6.  Run the following command to disable logout on system timeout:

    **TMOUT=0**

7.  Run the following command to go to the related directory:

    **cd ${HOME}/.ssh**

8.  Run the following command to add new public keys:

    **cat id_rsa.pub_bak >> authorized_keys**

9.  Run the following command to move the temporary public key file, for example, **/tmp**.

    **mv -f id_rsa.pub_bak** **/tmp**

10. Copy the **authorized_keys** file of the active management node to the other nodes in the cluster:

    **scp authorized_keys** *node_ip*\ **:/${HOME}/.ssh/authorized_keys**

    *node_ip*: indicates the IP address of another node in the cluster. Multiple IP addresses are not supported.

11. Run the following command to confirm private key replacement without entering the password:

    **ssh** *node_ip*

    *node_ip*: indicates the IP address of another node in the cluster. Multiple IP addresses are not supported.

12. Log in to FusionInsight Manager. On **Homepage**, locate the desired cluster and choose |image1| > **Start** to start the cluster.

.. |image1| image:: /_static/images/en-us_image_0263899299.png
