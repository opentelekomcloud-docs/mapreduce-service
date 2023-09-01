:original_name: ALM-24003.html

.. _ALM-24003:

ALM-24003 Flume Client Connection Interrupted
=============================================

Description
-----------

The alarm module monitors the port connection status on the Flume server. This alarm is generated if the Flume server fails to receive a connection message from the Flume client in three consecutive minutes.

This alarm is cleared after the Flume server receives a connection message from the Flume client.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
24003    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+---------------------------------------------------------+
| Name              | Meaning                                                 |
+===================+=========================================================+
| Source            | Specifies the cluster for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| Client IP Address | Specifies the IP address of the Flume client.           |
+-------------------+---------------------------------------------------------+
| Client Name       | Specifies the agent name of the Flume client.           |
+-------------------+---------------------------------------------------------+
| Sink Name         | Specifies the sink name of Flume Agent.                 |
+-------------------+---------------------------------------------------------+

Impact on the System
--------------------

The communication between the Flume client and the server fails. The Flume client cannot send data to the Flume server.

Possible Causes
---------------

-  The network connection between the Flume client and the server is faulty.
-  The Flume client's process is abnormal.
-  The Flume client is incorrectly configured.

Procedure
---------

**Check the network connection between the Flume client and the server.**

#. Log in to the host whose IP address is specified by **Flume ClientIP** in the alarm information as user **root**.
#. Run the **ping** *Flume server IP address* command to check whether the network connection between the Flume client and the server is normal.

   -  If yes, go to :ref:`3 <alm-24003__li331072891100>`.
   -  If no, go to :ref:`11 <alm-24003__li228207951100>`.

**Check whether the Flume client's process is normal.**

3. .. _alm-24003__li331072891100:

   Log in to the host whose IP address is specified by **Flume ClientIP** in the alarm information as user **root**.

4. Run the **ps -ef|grep flume \|grep client** command to check whether the Flume client process exists.

   -  If yes, go to :ref:`5 <alm-24003__li540399381100>`.
   -  If no, go to :ref:`11 <alm-24003__li228207951100>`.

**Check the Flume client configuration.**

5. .. _alm-24003__li540399381100:

   Log in to the host whose IP address is specified by **Flume ClientIP** in the alarm information as user **root**.

6. Run the **cd** *Flume client installation directory*\ **/fusioninsight-flume-1.9.0/conf/** command to go to Flume's configuration directory.

7. Run the **cat properties.properties** command to query the current configuration file of the Flume client.

8. Check whether the **properties.properties** file is correctly configured according to the configuration description of the Flume agent.

   -  If yes, go to :ref:`9 <alm-24003__li636773281100>`.
   -  If no, go to :ref:`11 <alm-24003__li228207951100>`.

9. .. _alm-24003__li636773281100:

   Modify the **properties.properties** configuration file.

**Check whether the alarm is cleared.**

10. Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-24003__li228207951100>`.

**Collect the fault information.**

11. .. _alm-24003__li228207951100:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

12. Expand the **Service** drop-down list, and select **Flume** for the target cluster.

13. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Collect logs in the **/var/log/Bigdata/flume-client** directory on the Flume client using a transmission tool.

15. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532767398.png
