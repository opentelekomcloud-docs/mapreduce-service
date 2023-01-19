:original_name: mrs_01_0859.html

.. _mrs_01_0859:

Using CGroups with YARN
=======================

Scenario
--------

CGroups is a Linux kernel feature. In YARN this feature allows containers to be limited in their resource usage (example, CPU usage). Without CGroups, it is hard to limit the container CPU usage. Without CGroups, it is hard to limit the container CPU usage.

.. note::

   Currently, CGroups is only used for limiting the CPU usage.

Configuration Description
-------------------------

CGroups is a Linux kernel feature and is enabled by using LinuxContainerExecutor. For details about how to configure the LinuxContainerExecutor for security, see the official website. You can learn the file system permissions assigned for users and user groups from documentation published on the official website.

.. note::

   -  Do not modify users, user groups, and related permissions of various paths in the corresponding file system. Otherwise, functions of CGroups may become abnormal.
   -  If the parameter value of **yarn.nodemanager.resource.percentage-physical-cpu-limit** is too small, the number of available cores may be less than one. For example, if the parameter of a four-core node is set to 20%, the number available core is less than one. As a result, all cores will be used. The Quota mode can be used in Linux versions, for example, Cent OS, that do not support Quota mode.

The table below describes the parameter for configuring cpuset mode, that is, only configured CPUs can be used by YARN.

.. _mrs_01_0859__en-us_topic_0000001219029361_t97b2bd7c74a543f8a43145ddc28e1af0:

.. table:: **Table 1** Parameter description

   +-----------------------------------------------------------------+------------------------------------------------------------------------------------------------------+---------------+
   | Parameter                                                       | Description                                                                                          | Default Value |
   +=================================================================+======================================================================================================+===============+
   | yarn.nodemanager.linux-container-executor.cgroups.cpu-set-usage | Whether to enable the cpuset mode. If this parameter is set to **true**, the cpuset mode is enabled. | false         |
   +-----------------------------------------------------------------+------------------------------------------------------------------------------------------------------+---------------+

The table below describes the parameters for configuring the strictcpuset mode, that is, only configured CPUs can be used by containers.

.. _mrs_01_0859__en-us_topic_0000001219029361_td100d24aaa184229963c9bf6323c0ea5:

.. table:: **Table 2** Parameter description

   +-------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------+---------------+
   | Parameter                                                               | Description                                                                                                            | Default Value |
   +=========================================================================+========================================================================================================================+===============+
   | yarn.nodemanager.linux-container-executor.cgroups.cpu-set-usage         | Whether to enable the cpuset mode. If this parameter is set to **true**, the cpuset mode is enabled.                   | false         |
   +-------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------+---------------+
   | yarn.nodemanager.linux-container-executor.cgroups.cpuset.strict.enabled | Whether containers use allocated CPUs. If this parameter is set to **true**, the container can use the allocated CPUs. | false         |
   +-------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------+---------------+

To switch from cpuset mode to quota mode, the following conditions must be met:

-  Set the **yarn.nodemanager.linux-container-executor.cgroups.cpu-set-usage** parameter to **false**.
-  Delete container folders if exists.
-  Delete all the CUPs configured in the **cpuset.cpus** file.

Procedure
---------

#. Log in to Manager. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Yarn** > **Configurations** and select **All Configurations**.

#. In the navigation pane on the left, choose **NodeManager** > **Customization** and find the **yarn-site.xml** file.

#. Add the parameters in :ref:`Table 1 <mrs_01_0859__en-us_topic_0000001219029361_t97b2bd7c74a543f8a43145ddc28e1af0>` and :ref:`Table 2 <mrs_01_0859__en-us_topic_0000001219029361_td100d24aaa184229963c9bf6323c0ea5>` as user-defined parameters.

   Based on the configuration files and parameter functions, locate the row where parameter **yarn-site.xml** resides. Enter the parameter name in the **Name** column and enter the parameter value in the **Value** column.

   Click **+** to add a customized parameter.

#. Click **Save**. In the displayed **Save Configuration** dialog box, confirm the modification and click **OK**. Click **Finish** when the system displays "Operation succeeded". The configuration is successfully saved.

   After the configuration is saved, restart the Yarn service whose configuration has expired for the configuration to take effect.
