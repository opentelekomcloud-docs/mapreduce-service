:original_name: ALM-12040.html

.. _ALM-12040:

ALM-12040 Insufficient System Entropy
=====================================

Description
-----------

MRS 3.2.0-LTS.2 or later:

The system checks whether the rng-tools or haveged tool has been enabled and correctly configured every 5 minutes. If neither tool is configured, this alarm is generated. If either is configured, the system continues to check the entropy. If the entropy is less than 100 for five consecutive times, this alarm is generated.

This alarm is cleared when rng-tools or haveged has been installed and enabled on the target node and the entropy of the OS is greater than or equal to 100 in at least one of five entropy checks.

MRS 3.1.2-LTS.6 or earlier:

The system checks the entropy for five consecutive times at 00:00 every day. Specifically, the system checks whether rng-tools or haveged has been enabled and correctly configured. If neither is configured, the system continues to check the entropy. If the entropy is less than 100 for five consecutive times, this alarm is reported.

This alarm is cleared when the system detects that the true random number mode has been configured, the random number parameters have been configured in the pseudo-random number mode, or neither mode is configured but the entropy of the OS is greater than or equal to 100 in at least one of five entropy checks.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12040    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+-------------------------------------------------------------------+
| Name        | Meaning                                                           |
+=============+===================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated. |
+-------------+-------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.           |
+-------------+-------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

The system is not running properly.

Possible Causes
---------------

-  rng-tools or haveged has not been installed or started.
-  The entropy of the OS is smaller than 100 for multiple consecutive times.

Procedure
---------

**Check whether haveged or rng-tools has been installed or started.**

#. Log in to MRS Manager and choose **O&M** > **Alarm** > **Alarms**.

#. Check the value of **HostName** in the **Location** area to obtain the name of the host for which the alarm is generated.

#. Log in to the node for which the alarm is generated as user **root**.

#. Run the **/bin/rpm -qa \| grep -w "haveged"** command to check the haveged installation status and check whether the command output is empty.

   -  If yes, go to :ref:`6 <alm-12040__li978924652119>`.
   -  If no, go to :ref:`5 <alm-12040__li35057727105655>`.

#. .. _alm-12040__li35057727105655:

   Run the **/sbin/service haveged status \|grep "running"** command and check the command output.

   -  If the command is executed successfully, haveged has been installed and configured correctly and is running properly. Go to :ref:`8 <alm-12040__li22912175218>`.

   -  If the command fails to execute, haveged is not running properly. Run the following command to manually restart haveged and go to :ref:`9 <alm-12040__li20231214524>`:

      **systemctl restart haveged.service**

#. .. _alm-12040__li978924652119:

   Run the **/bin/rpm -qa \| grep -w "rng-tools"** command to check the rng-tools installation and check whether the command output is empty.

   -  If yes, contact the OS vendor to install and start haveged or rng-tools. Then go to :ref:`9 <alm-12040__li20231214524>`.
   -  If no, go to :ref:`7 <alm-12040__li34867421105655>`.

#. .. _alm-12040__li34867421105655:

   Run the **ps -ef \| grep -v "grep" \| grep rngd \| tr -d " " \| grep "\\-r/dev/urandom"** command and check the command output.

   -  If the command is executed successfully, rngd has been installed and configured correctly and is running properly. Go to :ref:`8 <alm-12040__li22912175218>`.

   -  If the command fails to execute, rngd is not running properly. Run the following command to manually restart rngd and go to :ref:`9 <alm-12040__li20231214524>`:

      **systemctl restart rngd.service**

**Check the entropy of the OS.**

8. .. _alm-12040__li22912175218:

   Manually check the entropy of the OS.

   Log in to the target node as user **root** and run the **cat /proc/sys/kernel/random/entropy_avail** command to check whether the entropy of the OS meets cluster installation requirements (no less than 100).

   -  If yes, the entropy of the OS is not less than 100. Go to :ref:`9 <alm-12040__li20231214524>`.
   -  If no, the entropy of the OS is less than 100. Use either of the following methods and go to :ref:`9 <alm-12040__li20231214524>`.

      -  Method 1: Use haveged (true random number mode). Contact the OS vendor to install and start haveged.

         In Kylin, run the following command:

         **vi /usr/lib/systemd/system/haveged.service**

         Configure **Type**, **ExecStar**, **SuccessExitStatus**, and **Restart** in **[Service]** as follows:

         .. code-block::

            Type=simple
            ExecStar=/usr/sbin/haveged -w 1024 -v 1 -Foreground
            SuccessExitStatus=137 143
            Restart=always

      -  Method 2: Use rng-tools (pseudo-random number mode). Contact the OS vendor to install and start rng-tools and configure it based on the OS type.

         -  In Red Hat Linux or CentOS, run the following commands:

            **echo 'EXTRAOPTIONS="-r /dev/urandom -o /dev/random -t 1 -i"' >> /etc/sysconfig/rngd**

            **service rngd start**

            **chkconfig rngd on**

         -  In SUSE, run the following commands:

            **rngd -r /dev/urandom -o /dev/random**

            **echo "rngd -r /dev/urandom -o /dev/random" >> /etc/rc.d/after.local**

         -  In Kylin, run the following command as user **root** on the node where the alarm is reported:

            **vi /usr/lib/systemd/system/rngd.service**

            Change the value of **ExecStart** in **[Service]** as follows:

            .. code-block::

               ExecStart=/sbin/rngd -f -r /dev/urandom -s 2048

9. .. _alm-12040__li20231214524:

   Wait until the system to check the entropy at 00:00 on the following day and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-12040__li5962839105655>`.

**Collect fault information.**

10. .. _alm-12040__li5962839105655:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

11. Select **NodeAgent** for **Service** and click **OK**.

12. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

13. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

.. |image1| image:: /_static/images/en-us_image_0000001532927350.png
