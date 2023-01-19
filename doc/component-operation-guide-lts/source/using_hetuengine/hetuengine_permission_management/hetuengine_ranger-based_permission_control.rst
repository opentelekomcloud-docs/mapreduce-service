:original_name: mrs_01_1723.html

.. _mrs_01_1723:

HetuEngine Ranger-based Permission Control
==========================================

Newly installed clusters use Ranger for authentication by default. System administrators can use Ranger to configure the permissions to manage databases, tables, and columns of data sources for HetuEngine users. For details, see :ref:`Adding a Ranger Access Permission Policy for HetuEngine <mrs_01_1862>`.

If a cluster is upgraded from an earlier version or Ranger authentication is manually disabled for a cluster, enable Ranger authentication again by referring to :ref:`Enabling Ranger Authentication <mrs_01_1723__en-us_topic_0000001219351179_section622553792416>`.

.. _mrs_01_1723__en-us_topic_0000001219351179_section622553792416:

Enabling Ranger Authentication
------------------------------

#. Log in to FusionInsight Manager.
#. Choose **Cluster** > **Services** > **HetuEngine** > **More** > **Enable Ranger**.
#. Choose **Cluster** > **Services** > **HetuEngine** > **More** > **Restart Service**.
#. Restart the compute instance on HSConsole. For details, see :ref:`Managing a HetuEngine Compute Instance <mrs_01_1736>`.
