:original_name: mrs_01_1850.html

.. _mrs_01_1850:

Logging In to the Ranger Web UI
===============================

Ranger provides a centralized permission management framework to implement fine-grained permission control on components such as HDFS, HBase, Hive, and Yarn. In addition, Ranger also provides a web UI for system administrators to perform operations.

.. _mrs_01_1850__en-us_topic_0000001219350647_section2695135412818:

Ranger User Type
----------------

Ranger users are classified into **admin**, **user**, and **auditor**. Different users have different permissions to view and operate the Ranger management interface.

-  **Admin**: A security administrator can view all page content, manage permission management plug-ins and access control policies, view audit information, and set user types.
-  **Auditor**: An audit administrator can view the permission management plug-ins and access control policies.
-  **User**: A common user who can be assigned with specific permissions by the system administrator.


Logging In to the Ranger Web UI
-------------------------------

Security mode (Kerberos authentication is enabled for clusters)

#. Log in to FusionInsight Manager as user **admin**. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > **Services** > **Ranger**. The Ranger service overview page is displayed.
#. Click **RangerAdmin** in the **Basic Information** area. The Ranger web UI is displayed.

   -  The **admin** user in Ranger belongs to the **User** type and can only view the **Access Manager** as well as **Security Zone** pages.
   -  To view all management pages, switch to user **rangeradmin** or other users who have the Ranger administrator permissions.

      a. On the Ranger WebUI, click the user name in the upper right corner and choose **Log Out** to log out of the Ranger WebUI.

         |image1|

      b. Log in to the system as user **rangeradmin** or another user who has the Ranger administrator permissions. For details about the usernames and default passwords, contact the system administrator.

Normal mode (Kerberos authentication is disabled for clusters)

#. Log in to FusionInsight Manager as user **admin**. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > **Services** > **Ranger**. The Ranger service overview page is displayed.

#. Click **RangerAdmin** in the **Basic Information** area. The Ranger web UI is displayed.

   The **admin** user in Ranger belongs to the **Admin** type and can view all management pages of Ranger withour switching to user **rangeradmin**.

   .. note::

      When a user logs in to the Ranger WebUI as user **rangeradmin** in normal mode, error 401 is reported.

On the homepage of Ranger web UI, you can view the permission management plug-ins of the services integrated in Ranger. The plug-ins can be used to set more fine-grained permissions. For details about functions of main operations you can perform on the page, see :ref:`Table 1 <mrs_01_1850__en-us_topic_0000001219350647_t2e8dff27d0214c0885ce9fa207af6953>`.

.. _mrs_01_1850__en-us_topic_0000001219350647_t2e8dff27d0214c0885ce9fa207af6953:

.. table:: **Table 1** Functions of each operation portal on the Ranger page

   +----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Portal         | Function                                                                                                                                                                                                                                                                        |
   +================+=================================================================================================================================================================================================================================================================================+
   | Access Manager | You can view the permission management plug-ins of each service integrated in Ranger. The plug-ins can be used to set more fine-grained permissions. For details, see :ref:`Configuring Component Permission Policies <mrs_01_1851>`.                                           |
   +----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Audit          | You can view the audit logs related to Ranger running and permission control. For details, see :ref:`Viewing Ranger Audit Information <mrs_01_1852>`.                                                                                                                           |
   +----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Security Zone  | System administrators can divide resources of each component into multiple security zones where different administrators set security policies for specified resources of services to facilitate management. For details, see :ref:`Configuring a Security Zone <mrs_01_1853>`. |
   +----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Settings       | You can view Ranger permission settings, such as users, user groups, and roles. For details, see :ref:`Viewing Ranger Permission Information <mrs_01_1854>`.                                                                                                                    |
   +----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001389506524.png
