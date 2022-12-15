:original_name: alm_12040.html

.. _alm_12040:

ALM-12040 Insufficient System Entropy
=====================================

Description
-----------

The system checks the entropy at 00:00:00 every day and performs five consecutive checks each time. First, the system checks whether the rng-tools tool is enabled and correctly configured. If not, the system checks the current entropy. This alarm is generated if the entropy is less than 500 in the five checks.

This alarm is cleared if the true random number mode is configured, random numbers are configured in pseudo-random number mode, or neither the true random number mode nor the pseudo-random number mode is configured but the entropy is greater than or equal to 500 in at least one check among the five checks.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12040    Major          Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Parameter   Description
=========== =======================================================
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

Decryption failures occur and functions related to decryption are affected, for example, DBService installation.

Possible Causes
---------------

The rngd service is abnormal.

Procedure
---------

#. Go to the cluster details page and choose **Alarms**.

#. View the alarm details to obtain the value of the **HostName** field in **Location**.

#. Log in to the node for which the alarm is generated and run the **sudo su - root** command to switch to user **root**.

#. Run the **/bin/rpm -qa \| grep -w "rng-tools"** command. If the command is executed successfully, run the **ps -ef \| grep -v "grep" \| grep rngd \| tr -d " " \| grep "\\-o/dev/random" \| grep "\\-r/dev/urandom"** command and view the command output.

   -  If the command is executed successfully, the rngd service is installed, correctly configured, and is running properly. Go to :ref:`8 <alm_12040__en-us_topic_0191813866_li572522141314>`.
   -  If the command is not executed successfully, the rngd service is not running properly. Then go to :ref:`5 <alm_12040__en-us_topic_0191813866_li73201122101210>`.

#. .. _alm_12040__en-us_topic_0191813866_li73201122101210:

   Run the following command to start the rngd service:

   **echo 'EXTRAOPTIONS="-r /dev/urandom -o /dev/random"' >> /etc/sysconfig/rngd**

   **service rngd start**

#. Run the **service rngd status** command to check whether the rngd service is in the running state.

   -  If yes, go to :ref:`7 <alm_12040__en-us_topic_0191813866_li11437156145229>`.
   -  If no, go to :ref:`8 <alm_12040__en-us_topic_0191813866_li572522141314>`.

#. .. _alm_12040__en-us_topic_0191813866_li11437156145229:

   Wait until 00:00:00 when the system checks the entropy again. Check whether the alarm is cleared automatically.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm_12040__en-us_topic_0191813866_li572522141314>`.

#. .. _alm_12040__en-us_topic_0191813866_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
