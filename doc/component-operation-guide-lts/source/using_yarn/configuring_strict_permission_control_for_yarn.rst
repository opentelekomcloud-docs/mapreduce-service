:original_name: mrs_01_0857.html

.. _mrs_01_0857:

Configuring Strict Permission Control for Yarn
==============================================

Scenario
--------

In the multi-tenant scenario in security mode, a cluster can be used by multiple users, and tasks of multiple users can be submitted and executed. Users are invisible to each other. A permission control mechanism is required to prevent task information of users from being obtained by other users.

For example, if user B logs in to the system and views the application list when the application submitted by user A is running, user B should not be able to view the application information of user A.

Configuration Description
-------------------------

-  Viewing Yarn configuration parameters

   Go to the **All Configurations** page of Yarn and enter a parameter name list in :ref:`Table 1 <mrs_01_0857__en-us_topic_0000001219351155_table34313276373>` in the search box by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.

   .. _mrs_01_0857__en-us_topic_0000001219351155_table34313276373:

   .. table:: **Table 1** Parameter description

      +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Parameter                              | Description                                                                                                                                                                                                                | Default Value |
      +========================================+============================================================================================================================================================================================================================+===============+
      | yarn.acl.enable                        | Whether to enable Yarn permission control                                                                                                                                                                                  | true          |
      +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | yarn.webapp.filter-entity-list-by-user | Whether to enable the strict view function. After this function is enabled, a login user can view only the content that the user has the permission to view. To enable this function, set **yarn.acl.enable** to **true**. | true          |
      +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+

-  Viewing MapReduce configuration parameters

   Go to the **All Configurations** page of MapReduce and enter a parameter name in :ref:`Table 2 <mrs_01_0857__en-us_topic_0000001219351155_table183214752115>` in the search box by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.

   .. _mrs_01_0857__en-us_topic_0000001219351155_table183214752115:

   .. table:: **Table 2** Parameter description

      +----------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Parameter                              | Description                                                                                                                                                                                                                                                                                                                                                                                                                         | Default Value |
      +========================================+=====================================================================================================================================================================================================================================================================================================================================================================================================================================+===============+
      | mapreduce.cluster.acls.enabled         | Whether to enable permission control of MapReduce JobHistoryServer This parameter is a client parameter and takes effect after permission control is enabled on the JobHistoryServer server.                                                                                                                                                                                                                                        | true          |
      +----------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | yarn.webapp.filter-entity-list-by-user | Whether to enable the strict view of MapReduce JobHistoryServer. After the strict view is enabled, a login user can view only the content that the user has the permission to view. This parameter is a server parameter of JobHistoryServer. It indicates that permission control is enabled for JHS. However, whether to control a specific application is determined by the client parameter **mapreduce.cluster.acls.enabled**. | true          |
      +----------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+

   .. important::

      The preceding configurations affect the RESTful API and Shell command results. After the preceding configurations are enabled, the return results of RESTful API calls and shell commands contain only the information that the user has the permission to view.

      If **yarn.acl.enable** or **mapreduce.cluster.acls.enabled** is set to **false**, the Yarn or MapReduce permission verification function is disabled. In this case, any user can submit tasks and view task information on Yarn or MapReduce, which poses security risks. Exercise caution when performing this operation.
