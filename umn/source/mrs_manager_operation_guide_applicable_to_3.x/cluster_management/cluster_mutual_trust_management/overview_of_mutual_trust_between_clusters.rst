:original_name: admin_guide_000175.html

.. _admin_guide_000175:

Overview of Mutual Trust Between Clusters
=========================================

Function Description
--------------------

By default, users of a big data cluster in security mode can only access resources in the cluster but cannot perform identity authentication or access resources in other clusters in security mode.

Feature Description
-------------------

-  **Domain**

   The secure usage scope of users in each system is called a domain. Each MRS Manager must have a unique domain name. Cross-Manager access allows users to use resources across domains.

-  **User Encryption**

   Mutual trust can be configured across MRS Managers. The current Kerberos server supports only the aes256-cts-hmac-sha1-96:normal and aes128-cts-hmac-sha1-96:normal encryption types for encrypting cross-domain users, and the encryption types cannot be changed.

-  **User Authentication**

   After cross-Manager mutual trust is configured, if a user with the same name exists in two systems and the user in the peer system has the permission to access a resource in that system, this user can also access the remote resource.

-  **Direct Mutual Trust**

   The system saves the mutual trust ticket of the peer system in two clusters with mutual trust configured and uses the mutual trust ticket to access the peer system.
