:original_name: mrs_01_2346.html

.. _mrs_01_2346:

Configuring SSL for the HA Module
=================================

Scenario
--------

This section describes how to manually configure SSL for the HA module of DBService in the cluster where DBService is installed.

.. note::

   After this operation is performed, if you need to restore the SSL configuration, go to :ref:`Restoring SSL for the HA Module <mrs_01_2347>`.

Prerequisites
-------------

-  The cluster has been installed.
-  The **root-ca.crt** and **root-ca.pem** files in the **$BIGDATA_HOME/FusionInsight_BASE\_**\ *x.x.x*\ **/install/FusionInsight-dbservice-2.7.0/security** directory on the active and standby DBService nodes are the same.

Procedure
---------

#. Log in to the DBService node where SSL needs to be configured as user **omm**.

#. .. _mrs_01_2346__en-us_topic_0000001173471440_li1682110356353:

   Go to the **$BIGDATA_HOME/FusionInsight_BASE\_**\ *x.x.x*\ **/install/FusionInsight-dbservice-2.7.0/sbin/** directory and run the following command:

   **./proceed_ha_ssl_cert.sh** *DBService* *installation directoryService IP address of the node*

   Example:

   **cd $BIGDATA_HOME/FusionInsight_BASE\_**\ *x.x.x*\ **/install/FusionInsight-dbservice-2.7.0/sbin/**

   **./proceed_ha_ssl_cert.sh $BIGDATA_HOME/FusionInsight_BASE\_**\ *x.x.x*\ **/install/FusionInsight-dbservice-2.7.0** **10.10.10.10**

   .. note::

      **$BIGDATA_HOME/FusionInsight_BASE\_**\ *x.x.x*\ **/install/FusionInsight-dbservice-2.7.0** is the installation directory of DBService. Modify it based on site requirements.

#. Go to the **$BIGDATA_HOME/FusionInsight_BASE\_**\ *x.x.x*\ **/install/FusionInsight-dbservice-2.7.0/ha/module/hacom/script/** directory and run the following command to restart the HA process:

   **./stop_ha.sh**

   **./start_ha.sh**

#. Run the following command on the preceding node to obtain the PID of the HA process:

   **ps -ef \|grep "ha.bin" \|grep DBSERVICE**

#. Run the following command to check whether the protocol is changed to TCP:

   **netstat -nap \| grep** *pid* **\|** **grep -v unix**

   -  If yes, no further action is required.
   -  If no, go to :ref:`2 <mrs_01_2346__en-us_topic_0000001173471440_li1682110356353>`.

   .. code-block::

      (Not all processes could be identified, non-owned process info
       will not be shown, you would have to be root to see it all.)
      tcp        0      0 127.0.0.1:20054         0.0.0.0:*               LISTEN      11896/ha.bin
      tcp        0      0 10.10.10.10:20052   10.10.10.14:20052        ESTABLISHED    11896/ha.bin
      tcp        0      0 10.10.10.10:20053   10.10.10.14:20053        ESTABLISHED    11896/ha.bin
