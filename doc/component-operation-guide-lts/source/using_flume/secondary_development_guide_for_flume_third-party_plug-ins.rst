:original_name: mrs_01_1083.html

.. _mrs_01_1083:

Secondary Development Guide for Flume Third-Party Plug-ins
==========================================================

Scenario
--------

This section describes how to perform secondary development for third-party plug-ins.

Prerequisites
-------------

-  You have obtained the third-party JAR package.

-  You have installed Flume server or client.

Procedure
---------

#. Compress the self-developed code into a JAR package.

#. Create a directory for the plug-in.

   a. Access the **$FLUME_HOME/plugins.d** path and run the following command to create a directory:

      **mkdir thirdPlugin**

      **cd thirdPlugin**

      **mkdir lib libext** **native**

      The command output is displayed as follows:

      |image1|

   b. Place the third-party JAR package in the **$FLUME_HOME/plugins.d/thirdPlugin/lib** directory. If the JAR package depends on other JAR packages, place the depended JAR packages to the **$FLUME_HOME/ plugins.d/ thirdPlugin/libext** directory, and place the local library files in **$FLUME_HOME/ plugins.d/ thirdPlugin/native**.

#. Configure the **properties.properties** file in **$FLUME_HOME/conf/**.

   For details about how to set parameters in the **properties.properties** file, see the parameter list in the **properties.properties** file in the corresponding typical scenario :ref:`Non-Encrypted Transmission <mrs_01_1059>` and :ref:`Encrypted Transmission <mrs_01_1068>`.

   .. note::

      -  **$FLUME_HOME** indicates the Flume installation path. Set this parameter based on the site requirements (server or client) when configuring third-party plug-ins.
      -  **thirdPlugin** is the name of the third-party plugin.

.. |image1| image:: /_static/images/en-us_image_0000001441209301.png
