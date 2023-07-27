:original_name: ALM-24001.html

.. _ALM-24001:

ALM-24001 Flume Agent Exception
===============================

Description
-----------

The Flume agent instance for which the alarm is generated cannot be started. This alarm is generated when the Flume agent process is faulty (The system checks in every 5 seconds.) or Flume agent fails to start (The system reporting alarms immediately).

This alarm is cleared when the Flume agent process recovers, Flume agent starts successfully and the alarm handling is completed.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
24001    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+-----------------------------------------------------------------+
| Name        | Meaning                                                         |
+=============+=================================================================+
| Source      | Specifies the cluster for which the alarm is generated.         |
+-------------+-----------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.         |
+-------------+-----------------------------------------------------------------+
| AgentId     | Specifies the ID of the agent for which the alarm is generated. |
+-------------+-----------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.            |
+-------------+-----------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.            |
+-------------+-----------------------------------------------------------------+

Impact on the System
--------------------

The Flume agent instance for which the alarm is generated cannot provide services properly, and the data transmission tasks of the instance are temporarily interrupted. Real-time data is lost during real-time data transmission.

Possible Causes
---------------

-  The JAVA_HOME directory does not exist or the Java permission is incorrect.
-  The Flume agent directory permission is incorrect.
-  Flume agent fails to start.

Procedure
---------

**Check whether the** **JAVA_HOME** **directory exists or whether the JAVA permission is correct.**

#. Log in to the host for which the alarm is generated as user **root**.

#. Run the following command to obtain the installation directory of the Flume client for which the alarm is generated: (The value of **AgentId** can be obtained from **Location** of the alarm.)

   **ps -ef|grep** *AgentId* **\| grep -v grep \| awk -F 'conf-file ' '{print $2}' \| awk -F 'fusioninsight' '{print $1}'**

#. Run the **su -** *Flume installation user* command to switch to the Flume installation user and run the **cd** *Flume client installation directory*\ **/fusioninsight-flume-1.9.0/conf/** command to go to the Flume configuration directory.

#. .. _alm-24001__li62419311105615:

   Run the **cat ENV_VARS \| grep JAVA_HOME** command.

#. Check whether the **JAVA_HOME** directory exists. If the command output in :ref:`4 <alm-24001__li62419311105615>` is not empty and **ll $JAVA_HOME/** is not empty, the **JAVA_HOME** directory exists.

   -  If yes, go to :ref:`7 <alm-24001__li1404949105615>`.
   -  If no, go to :ref:`6 <alm-24001__li28531951910>`.

#. .. _alm-24001__li28531951910:

   Specify a correct **JAVA_HOME** directory.

#. .. _alm-24001__li1404949105615:

   Run the **$JAVA_HOME/bin/java -version** command to check whether the Flume agent running user has the Java execution permission. If the Java version is displayed in the command output, the Java permission meets the requirement. Otherwise, the Java permission does not meet the requirement.

   -  If yes, go to :ref:`9 <alm-24001__li12942052171720>`.
   -  If no, go to :ref:`8 <alm-24001__li17575375105615>`.

      .. note::

         **JAVA_HOME** is the environment variable exported during Flume client installation. You can also go to *Flume client installation directory*\ **/fusioninsight-flume-1.9.0/conf** and run the **cat ENV_VARS \| grep JAVA_HOME** command to view the variable value.

#. .. _alm-24001__li17575375105615:

   Run the **chmod 750 $JAVA_HOME/bin/java** command to grant the Java execution permission to the Flume agent running user.

**Check the directory permission of the Flume agent.**

9.  .. _alm-24001__li12942052171720:

    Log in to the host for which the alarm is generated as user **root**.

10. Run the following command to switch to the Flume agent installation directory:

    **cd** *Flume client installation directory*\ **/fusioninsight-flume-1.9.0/conf/**

11. Run the **ls -al \* -R** command to check whether any file owner is the user who running the Flume agent.

    -  If yes, go to :ref:`12 <alm-24001__li62476305536>`.
    -  If no, run the **chown** command to change the file owner to the user who runs the Flume agent.

**Check the Flume agent configuration.**

12. .. _alm-24001__li62476305536:

    Run the **cat properties.properties \| grep spooldir** and **cat properties.properties \| grep TAILDIR** commands to check whether the Flume source type is spoolDir or tailDir. If any command output is displayed, the Flume source type is spoolDir or tailDir.

    -  If yes, go to :ref:`13 <alm-24001__li124343613141>`.
    -  If no, go to :ref:`17 <alm-24001__li7261720101519>`.

13. .. _alm-24001__li124343613141:

    Check whether the data monitoring directory exists.

    -  If yes, go to :ref:`15 <alm-24001__li155813021512>`.
    -  If no, go to :ref:`14 <alm-24001__li17447826131411>`.

       .. note::

          Run the **cat properties.properties \| grep spoolDir** command to view the spoolDir monitoring directory.

          |image1|

          Run the **cat properties.properties \| grep parentDir** command to view the tailDir monitoring directory.

          |image2|

14. .. _alm-24001__li17447826131411:

    Specify a correct data monitoring directory.

15. .. _alm-24001__li155813021512:

    Check whether the Flume agent user has the read, write, and execute permissions on the monitoring directory specified in :ref:`13 <alm-24001__li124343613141>`.

    -  If yes, go to :ref:`17 <alm-24001__li7261720101519>`.
    -  If no, go to :ref:`16 <alm-24001__li64671529111412>`.

       .. note::

          Go to the monitoring directory as the Flume running user. If files can be created, the Flume running user has the read, write, and execute permissions on the monitoring directory.

16. .. _alm-24001__li64671529111412:

    Run the **chmod 777** *Flume monitoring directory* command to grant the Flume agent running user the read, write, and execute permissions on the monitoring directory specified in :ref:`13 <alm-24001__li124343613141>`.

17. .. _alm-24001__li7261720101519:

    Check whether the components connected to the Flume sink are in safe mode.

    -  If yes, go to :ref:`18 <alm-24001__li922422181513>`.
    -  If no, go to :ref:`23 <alm-24001__li28033577105615>`.

       .. note::

          If the sinks in the **properties.properties** configuration file are the HDFS sink and HBase sink, and the configuration file contains a keytab file, the components connected to the Flume sink are in safe mode.

          If the sink in the **properties.properties** configuration file is the kafka sink and **\*.security.protocol** is set to **SASL_PLAINTEXT** or **SASL_SSL**, Kafka connected to the Flume sink is in safe mode.

18. .. _alm-24001__li922422181513:

    Run the **ll** *ketab path* command to check whether the keytab authentication path specified by the **\*.kerberosKeytab** parameter in the configuration file exists.

    -  If yes, go to :ref:`20 <alm-24001__li485841172212>`.
    -  If no, go to :ref:`19 <alm-24001__li13851168209>`.

       .. note::

          To view the ketab path, run the **cat properties.properties \| grep keytab** command.

          |image3|

19. .. _alm-24001__li13851168209:

    Change the value of **kerberosKeytab** in :ref:`18 <alm-24001__li922422181513>` to the custom keytab path and go to :ref:`21 <alm-24001__li12245192314156>`.

20. .. _alm-24001__li485841172212:

    Perform :ref:`18 <alm-24001__li922422181513>` to check whether the Flume agent running user has the permission to access the keytab authentication file. If the keytab path is returned, the user has the permission. Otherwise, the user does not have the permission.

    -  If yes, go to :ref:`22 <alm-24001__li8869032152012>`.
    -  If no, go to :ref:`21 <alm-24001__li12245192314156>`.

21. .. _alm-24001__li12245192314156:

    Run the **chmod 755** *ketab file* command to grant the read permission on the keytab file specified in :ref:`19 <alm-24001__li13851168209>`, and restart the Flume process.

22. .. _alm-24001__li8869032152012:

    Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`23 <alm-24001__li28033577105615>`.

**Collect the fault information.**

23. .. _alm-24001__li28033577105615:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

24. Expand the **Service** drop-down list, and select **Flume** for the target cluster.

25. Click |image4| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

26. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583087521.png
.. |image2| image:: /_static/images/en-us_image_0000001582807813.png
.. |image3| image:: /_static/images/en-us_image_0000001532607870.png
.. |image4| image:: /_static/images/en-us_image_0000001583127505.png
