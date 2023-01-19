:original_name: mrs_01_2347.html

.. _mrs_01_2347:

Restoring SSL for the HA Module
===============================

Scenario
--------

This section describes how to restore SSL for the HA module of DBService in the cluster where DBService is installed.

Prerequisites
-------------

SSL has been enabled for the HA module of DBService.

.. note::

   Check whether SSL is enabled for the HA module of DBService.

   Check **$BIGDATA_HOME/FusionInsight_BASE\_**\ *x.x.x*\ **/install/FusionInsight-dbservice-2.7.0/ha/module/hacom/conf/hacom.xml**. If the file contains **<hadataprotocol value="ssl"></hadataprotocol>**, SSL is enabled.

Procedure
---------

#. Log in to the DBService node where SSL needs to be restored as user **omm**.

#. Run the following commands to restore the DBService configuration file **hacom_local.xml**:

   **cd $BIGDATA_HOME/FusionInsight_BASE\_**\ *x.x.x*\ **/install/FusionInsight-dbservice-2.7.0/ha/local/hacom/conf/**

   **cp hacom_local.xml $BIGDATA_HOME/tmp/**

   **cat hacom_local.xml \| grep "ssl>" -n \| cut -d':' -f1 \| xargs \| sed 's/ /,/g' \|xargs -n 1 -i sed -i '{}d' hacom_local.xm**\ l

#. Run the following commands to restore the DBService configuration file **hacom.xml**:

   **cd $BIGDATA_HOME/FusionInsight_BASE\_**\ *x.x.x*\ **/install/FusionInsight-dbservice-2.7.0/ha/module/hacom/conf/**

   **cp hacom.xml $BIGDATA_HOME/tmp/**

   **sed -i 's#<hadataprotocol.*#<hadataprotocol value="udp"/>#g' hacom.xml**

   **sed -i 's#<rpcsupportssl.*#<rpcsupportssl value="true"/>#g' hacom.xml**

   .. note::

      **$BIGDATA_HOME/FusionInsight_BASE\_**\ *x.x.x*\ **/install/FusionInsight-dbservice-2.7.0** is the installation directory of DBService. Modify it based on the upgrade environment.

#. Go to the **$BIGDATA_HOME/FusionInsight_BASE\_**\ *x.x.x*\ **/install/FusionInsight-dbservice-2.7.0/ha/module/hacom/script/** directory and run the following command to restart the HA process:

   **./stop_ha.sh**

   **./start_ha.sh**

#. Run the following command to obtain the PID of the HA process:

   **ps -ef \|grep "ha.bin" \|grep DBSERVICE**

#. Run the following command to check whether the protocol is changed to TCP:

   **netstat -nap \| grep** *pid* **\|** **grep -v unix**

   -  If yes, no further action is required.
   -  If no, contact O&M support.

   .. code-block:: console

      [omm@host03]\>netstat -nap | grep 49989
      (Not all processes could be identified, non-owned process info
       will not be shown, you would have to be root to see it all.)
      tcp        0      0 127.0.0.1:20054         0.0.0.0:*               LISTEN      49989/ha.bin
      udp        0      0 10.10.10.10:20052       0.0.0.0:*                           49989/ha.bin
      udp        0      0 10.10.10.10:20053       0.0.0.0:*                           49989/ha.bin
