:original_name: mrs_01_0347.html

.. _mrs_01_0347:

Locking a User
==============

This section describes how to lock users in MRS clusters. A locked user cannot log in to Manager or perform security authentication in the cluster. This operation is supported only in clusters with Kerberos authentication enabled or common clusters with the EIP function enabled.

A locked user can be unlocked by an administrator manually or until the lock duration expires. You can lock a user by using either of the following methods:

-  Automatic lock: Set **Number of Password Retries** in **Configure Password Policy**. If user login attempts exceed the parameter value, the user is automatically locked. For details, see :ref:`Modifying a Password Policy <mrs_01_0353>`.
-  Manual lock: The administrator manually locks a user.

.. note::

   The operations described in this section apply only to clusters of versions earlier than MRS 3.x.

   For clusters of **MRS 3.\ x** or later, see :ref:`Locking a User <admin_guide_000140>`.

The following describes how to manually lock a user. **Machine-machine** users cannot be locked.

Procedure
---------

#. Access MRS Manager. For details, see :ref:`Accessing MRS Manager MRS 2.1.0 or Earlier) <mrs_01_0102>`.
#. On MRS Manager, click **System**.
#. In the **Permission** area, click **Manage User**.
#. In the row of a user you want to lock, click **Lock User**.
#. In the window that is displayed, click **OK** to lock the user.
