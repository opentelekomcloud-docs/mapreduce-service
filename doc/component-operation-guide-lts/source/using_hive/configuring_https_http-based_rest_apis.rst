:original_name: mrs_01_0957.html

.. _mrs_01_0957:

Configuring HTTPS/HTTP-based REST APIs
======================================

Scenario
--------

WebHCat provides external REST APIs for Hive. By default, the open-source community version uses the HTTP protocol.

MRS Hive supports the HTTPS protocol that is more secure, and enables switchover between the HTTP protocol and the HTTPS protocol.

.. note::

   The security mode supports HTTPS and HTTP, and the common mode supports only HTTP.

Procedure
---------

#. The Hive service configuration page is displayed.

   Log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. And choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive** > **Configurations** > **All Configurations**.

#. Modify the Hive configuration.

   Choose **WebHCat** > **Security**. On the page that is displayed, select **HTTPS** or **HTTP**. After the modification, restart the Hive service to use the corresponding protocol.
