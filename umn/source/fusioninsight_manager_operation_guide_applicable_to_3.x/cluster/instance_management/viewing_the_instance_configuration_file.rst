:original_name: admin_guide_000044.html

.. _admin_guide_000044:

Viewing the Instance Configuration File
=======================================

Scenario
--------

FusionInsight Manager allows O&M personnel to view the content configuration files such as environment variables and role configurations of the instance node on the management page. If O&M personnel need to quickly check whether configuration items of the instance are incorrectly configured or when some hidden configuration items need to be viewed, the O&M personnel can directly view the configuration files on FusionInsight Manager. In this case, users quickly analyze configuration problems.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **Cluster** > *Name of the desired cluster* > **Service**.

#. Click the specified service name on the service management page. On the displayed page, click the **Instance** tab.

#. Click the name of the target instance. In the **Configuration File** area on the **Instance Status** page, the configuration file list of the instance is displayed.

#. Click the name of the configuration file to be viewed to view the parameter values in the configuration file.

   To obtain the configuration file, you can download the configuration file to the local PC.

   .. note::

      If a node in the cluster is faulty, the configuration file cannot be viewed. Rectify the fault before viewing the configuration file again.
