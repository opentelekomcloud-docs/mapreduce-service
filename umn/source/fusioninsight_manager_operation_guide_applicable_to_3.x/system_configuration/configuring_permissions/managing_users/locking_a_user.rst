:original_name: admin_guide_000140.html

.. _admin_guide_000140:

Locking a User
==============

Scenario
--------

A user may be suspended for a long period of time due to service changes. For security purposes, you can lock such a user.

You can lock a user in using either of the following methods:

-  Automatic locking: You can set **Password Retries** in the password policy to automatically lock the user whose login attempts exceed this parameter value. For details, see :ref:`Configuring Password Policies <admin_guide_000150>`.
-  Manual locking: You manually lock a user.

This section describes how to lock a user manually. Machine-machine users cannot be locked.

Impact on the System
--------------------

A locked user cannot log in to FusionInsight Manager or perform identity authentication in the cluster. A locked user can be used only after being manually unlocked or the lock time expires.

Procedure
---------

#. Log in to FusionInsight Manager.
#. Choose **System** > **Permission** > **User**.
#. Locate the row that contains the target user and click **Lock** in the **Operation** column.
#. In the window that is displayed, select **I have read the information and understand the impact**. Click **OK**.
