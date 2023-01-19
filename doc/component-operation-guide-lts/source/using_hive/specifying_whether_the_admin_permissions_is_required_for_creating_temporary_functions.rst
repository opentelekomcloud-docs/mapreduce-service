:original_name: mrs_01_0960.html

.. _mrs_01_0960:

Specifying Whether the **ADMIN** Permissions Is Required for Creating Temporary Functions
=========================================================================================

Scenario
--------

You must have **ADMIN** permission when creating temporary functions on Hive of the open source community version.

MRS Hive supports the configuration of the function for creating temporary functions with **ADMIN** permission. The function is disabled by default, which is the same as that of the open-source community version.

You can modify configurations of this function. After the function is enabled, you can create temporary functions without **ADMIN** permission. If this parameter is set to **false**, security risks exist.

.. note::

   The security mode supports the configuration of whether the ADMIN permission is required for creating temporary functions, but the common mode does not support this function.

Procedure
---------

#. Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > **Services** > **Hive** > **Configurations** > **All Configurations**.
#. Enter the parameter name in the search box, search for **hive.security.temporary.function.need.admin**, change the parameter value to **true** or **false**, and restart all HiveServer instances.

   .. note::

      -  If this parameter is set to **true**, the ADMIN permission is required for creating temporary functions, which is the same as that in the open source community.
      -  If this parameter is set to **false**, the ADMIN permission is not required for creating temporary functions.
