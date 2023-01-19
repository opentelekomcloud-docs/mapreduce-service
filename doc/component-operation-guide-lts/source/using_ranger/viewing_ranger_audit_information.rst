:original_name: mrs_01_1852.html

.. _mrs_01_1852:

Viewing Ranger Audit Information
================================

The system administrator can view audit logs of the Ranger running and the permission control after Ranger authentication is enabled on the Ranger web UI.


Viewing Ranger Audit Information
--------------------------------

#. Log in to the Ranger management page.

#. Click **Audit** to view the audit information. For details about the content on each tab page, see :ref:`Table 1 <mrs_01_1852__en-us_topic_0000001219230489_table774316265137>`. If there are a large number of items, click the search box and filter the items based on the keyword field.

   .. _mrs_01_1852__en-us_topic_0000001219230489_table774316265137:

   .. table:: **Table 1** Audit information

      +----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Tab            | Description                                                                                                                                                      |
      +================+==================================================================================================================================================================+
      | Access         | Records audit information about users' access to component resources through Ranger authentication.                                                              |
      +----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Admin          | Records operation audit information on Ranger, such as the creation, update, and deletion of security access policies, component permission policies, and roles. |
      +----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Login Sessions | Records session audit information for users who have logged in to Ranger.                                                                                        |
      +----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Plugins        | Records permission policy information of components in Ranger.                                                                                                   |
      +----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Plugin Status  | Records audit information about permission policies of each component node.                                                                                      |
      +----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | User Sync      | Records synchronized audit information of LDAP and Ranger users.                                                                                                 |
      +----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
