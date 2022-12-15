:original_name: admin_guide_000235.html

.. _admin_guide_000235:

Right Model
===========

Role-based Access Control
-------------------------

FusionInsight adopts the role-based access control (RBAC) mode to manage rights on the big data system. It integrates the right management functions of the components to centrally manage rights. Common users are shielded from internal right management details, and the right management operations are simplified for administrators, improving right management usability and user experience.

The right model of FusionInsight consists four parts, that is users, user groups, roles, and rights.


.. figure:: /_static/images/en-us_image_0263899538.png
   :alt: **Figure 1** Right model

   **Figure 1** Right model

-  **Right**

   Right, which is defined by components, allows users to access a certain resource of one component. Different components have different rights for their resources.

   For example:

   -  HDFS provides read, write, and execute permissions on files.
   -  HBase provides create, read, and write permissions on tables.

-  **Role**

   Role is a collection of component rights. Each role can have multiple rights of multiple components. Different roles can have the rights of a resource of one component.

-  **User group**

   User group is a collection of users. When a user group is bound to a role, users in this group obtain the rights defined by the role.

   Different user groups can be associated with the same role. A user group can also be associated with no role, and this user group does not have the rights of any component resources.

   .. note::

      In some components, the system grants related rights to specific user groups by default.

-  **User**

   A user is a visitor to the system. Each user has the rights of the user group and role associated with the user. Users need to be added to the user group or associated with roles to obtain the corresponding rights.

Policy-based Access Control
---------------------------

The Ranger component uses policy-based access control (PBAC) to manage rights and implement fine-grained data access control on components such as HDFS, Hive, and HBase.

.. note::

   The component supports only one right control mechanism. After the Ranger right control policy is enabled for the component, the right on the component in the role created on FusionInsight Manager becomes invalid (The ACL rules of HDFS and Yarn still take effect). You need to add a policy on the Ranger management page to grant rights on resources.

The Ranger right model consists of multiple right policies. A right policy consists of the following parts:

-  Resource

   Resources are provided by components and can be accessed by users, such as HDFS files or folders, queues in Yarn, and databases, tables, and columns in Hive.

-  User

   A User is a visitor to the system. The rights of each user are obtained based on the policy associated with the user. Information about users, user groups, and roles in the LDAP is periodically synchronized to the Ranger.

-  Permission

   In a policy, you can configure various access conditions for resources, such as file read and write, permission conditions, rejection conditions, and exception conditions.
