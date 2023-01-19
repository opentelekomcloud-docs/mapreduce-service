:original_name: mrs_01_1058.html

.. _mrs_01_1058:

Using Environment Variables in the **properties.properties** File
=================================================================

Scenario
--------

This section describes how to use environment variables in the **properties.properties** configuration file.

Prerequisites
-------------

The Flume service is running properly and the Flume client has been installed.

Procedure
---------

#. Log in to the node where the Flume client is installed as user **root**.

#. Switch to the following directory:

   **cd** *Flume client installation directory*/**fusioninsight-flume**\ ``-``\ *Flume component version*/**conf**

#. Add environment variables to the **flume-env.sh** file in the directory.

   -  Format:

      .. code-block::

         export Variable name=Variable value

   -  Example:

      .. code-block::

         JAVA_OPTS="-Xms2G -Xmx4G -XX:CMSFullGCsBeforeCompaction=1 -XX:+UseConcMarkSweepGC -XX:+CMSParallelRemarkEnabled -XX:+UseCMSCompactAtFullCollection -DpropertiesImplementation=org.apache.flume.node.EnvVarResolverProperties"
         export TAILDIR_PATH=/tmp/flumetest/201907/20190703/1/.*log.*

#. Restart the Flume instance process.

   a. Log in to FusionInsight Manager.
   b. Choose **Cluster** > **Services** > **Flume**. On the page that is displayed, click the **Instance** tab, select all Flume instances, and choose **More** > **Restart Instance**. In the displayed **Verify Identity** dialog box, enter the password, and click **OK**.

   .. important::

      Do not restart the Flume service on FusionInsight Manager after **flume-env.sh** takes effect on the server. Otherwise, the user-defined environment variables will lost. You only need to restart the corresponding instances on FusionInsight Manager.

#. .. _mrs_01_1058__li17459142018584:

   In the *Flume client installation directory*\ **/fusioninsight-flume-**\ *Flume component version number*\ **/conf/properties.properties** configuration file, reference variables in the **${**\ *Variable name*\ **}** format. The following is an example:

   .. code-block::

      client.sources.s1.type = TAILDIR
      client.sources.s1.filegroups = f1
      client.sources.s1.filegroups.f1 = ${TAILDIR_PATH}
      client.sources.s1.positionFile = /tmp/flumetest/201907/20190703/1/taildir_position.json
      client.sources.s1.channels = c1

   .. important::

      -  Ensure that **flume-env.sh** takes effect before you go to :ref:`5 <mrs_01_1058__li17459142018584>` to configure the **properties.properties** file.
      -  If you configure file on the local host, upload the file on FusionInsight Manager by performing the following steps. The user-defined environment variables may be lost if the operations are not performed in the correct sequence.

         a. Log in to FusionInsight Manager.
         b. Choose **Cluster** > **Services** > **Flume**. On the page that is displayed, click the **Configurations** tab, select the Flume instance, and click **Upload File** next to **flume.config.file** to upload the **properties.properties** file.
