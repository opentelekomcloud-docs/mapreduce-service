:original_name: admin_guide_000178.html

.. _admin_guide_000178:

Assigning User Permissions After Cross-Cluster Mutual Trust Is Configured
=========================================================================

Scenario
--------

After cross-Manager cluster mutual trust is configured, assign user access permissions on FusionInsight Managers so that these users can perform service operations in the mutually trusted Managers.

Prerequisites
-------------

The mutual trust between the two Managers has been configured.

Procedure
---------

#. Log in to the local FusionInsight Manager.

#. .. _admin_guide_000178__en-us_topic_0046737084_chk_user:

   Choose **System** > **Permission** > **User** to check whether the target user exists.

   -  If yes, go to :ref:`3 <admin_guide_000178__en-us_topic_0046737084_mod_user>`.
   -  If no, go to :ref:`4 <admin_guide_000178__en-us_topic_0046737084_add_user>`.

#. .. _admin_guide_000178__en-us_topic_0046737084_mod_user:

   Click |image1| on the left of the target user, and check whether the permissions assigned to the user group of the user and the roles meet service requirements. If not, create a role and bind the role to the user by referring to :ref:`Configuring Permissions <admin_guide_000135>`, or modify the user group or role permissions of the user.

#. .. _admin_guide_000178__en-us_topic_0046737084_add_user:

   Create a user required by the service operations and associate the required user group or role. For details, see :ref:`Creating a User <admin_guide_000137>`.

#. Log in to the other FusionInsight Manager and repeat :ref:`2 <admin_guide_000178__en-us_topic_0046737084_chk_user>` to :ref:`4 <admin_guide_000178__en-us_topic_0046737084_add_user>` to create a user with the same name and set permissions.

.. |image1| image:: /_static/images/en-us_image_0000001442413857.png
