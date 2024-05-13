:original_name: mrs_01_0349.html

.. _mrs_01_0349:

**Deleting a User**
===================

The administrator can delete an MRS cluster user that is not required on MRS Manager. Deleting a user is allowed only in clusters with Kerberos authentication enabled or normal clusters with the EIP function enabled.

.. note::

   If you want to create a new user with the same name as user A after deleting user A who has submitted a job on the client or MRS console, you need to delete user A's residual folders when deleting user A. Otherwise, the newly created user A may fail to submit a job.

   To delete residual folders, log in to each Core node in the MRS cluster and run the following commands. In the following commands, **$user** indicates the folder named after the username.

   **cd /srv/BigData/hadoop/data1/nm/localdir/usercache/**

   **rm -rf $user**

   The operations described in this section apply only to clusters of versions earlier than MRS 3.x.

   For clusters of **MRS 3.\ x** or later, see :ref:`Deleting a User <admin_guide_000142>`.

Procedure
---------

#. Access MRS Manager. For details, see :ref:`Accessing MRS Manager (MRS 2.x or Earlier) <mrs_01_0102>`.
#. On MRS Manager, click **System**.
#. In the **Permission** area, click **Manage User**.
#. In the row that contains the user to be deleted, choose **More** > **Delete**.
#. Click **OK**.
