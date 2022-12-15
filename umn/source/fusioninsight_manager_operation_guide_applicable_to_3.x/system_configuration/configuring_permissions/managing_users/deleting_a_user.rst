:original_name: admin_guide_000142.html

.. _admin_guide_000142:

Deleting a User
===============

Scenario
--------

Based on service requirements, you can delete system users that are no longer used on FusionInsight Manager.

.. note::

   -  After a user is deleted, the provisioned ticket granting ticket (TGT) is still valid within 24 hours. The user can use the TGT for security authentication and access the system.
   -  If a new user has the same name as the deleted user, the new user will inherit all owner permissions of the deleted user. You are advised to determine whether to delete the resources owned by the deleted user based on service requirements, for example, files in HDFS.
   -  The default user **admin** cannot be deleted.

Procedure
---------

#. Log in to FusionInsight Manager.
#. Choose **System** > **Permission** > **User**.
#. Locate the row that contains the target user, click **More**, and select **Delete**.

   .. note::

      To delete users in batches, select the users at a time and click **Delete**.

#. In the displayed dialog box, click **OK**.
