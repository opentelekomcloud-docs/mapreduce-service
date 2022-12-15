:original_name: mrs_01_0424.html

.. _mrs_01_0424:

Locking a User
==============

This section describes how to lock users in MRS clusters. A locked user cannot log in to MRS Manager or perform security authentication in the cluster.

A locked user can be unlocked by an administrator manually or until the lock duration expires. You can lock a user by using either of the following methods:

-  Automatic lock: Set **Number of Password Retries** in **Configure Password Policy**. If user login attempts exceed the parameter value, the user is automatically locked. For details, see :ref:`Modifying a Password Policy <mrs_01_0430>`.
-  Manual lock: The administrator manually locks a user.

The following describes how to manually lock a user. **Machine-Machine** users cannot be locked.

Procedure
---------

#. On MRS Manager, click **System**.
#. In the **Permission** area, click **Manage User**.
#. In the row of the user to be locked, click **Lock User**.
#. In the window that is displayed, click **Yes** to lock the user.
