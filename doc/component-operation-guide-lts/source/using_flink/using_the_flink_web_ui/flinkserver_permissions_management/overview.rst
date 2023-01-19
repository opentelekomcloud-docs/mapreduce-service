:original_name: mrs_01_24048.html

.. _mrs_01_24048:

Overview
========

User **admin** of Manager does not have the FlinkServer service operation permission. To perform FlinkServer service operations, you need to grant related permission to the user.

Applications (tenants) in FlinkServer are the maximum management scope, including cluster connection management, data connection management, application management, stream table management, and job management.

There are three types of resource permissions for FlinkServer, as shown in :ref:`Table 1 <mrs_01_24048__en-us_topic_0000001173949576_table663518214115>`.

.. _mrs_01_24048__en-us_topic_0000001173949576_table663518214115:

.. table:: **Table 1** FlinkServer resource permissions

   +--------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Name                                 | Description                                                                                                                                                             | Remarks                                                                                                                                                            |
   +======================================+=========================================================================================================================================================================+====================================================================================================================================================================+
   | FlinkServer administrator permission | Users who have the permission can edit and view all applications.                                                                                                       | This is the highest-level permission of FlinkServer. If you have the FlinkServer administrator permission, you have the permission on all applications by default. |
   +--------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Application edit permission          | Users who have the permission can create, edit, and delete cluster connections and data connections. They can also create stream tables as well as create and run jobs. | In addition, users who have the permission can view current applications.                                                                                          |
   +--------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Application view permission          | Users who have the permission can view applications.                                                                                                                    | ``-``                                                                                                                                                              |
   +--------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
