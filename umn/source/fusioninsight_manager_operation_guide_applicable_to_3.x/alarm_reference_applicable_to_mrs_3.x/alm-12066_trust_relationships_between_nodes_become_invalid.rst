:original_name: ALM-12066.html

.. _ALM-12066:

ALM-12066 Trust Relationships Between Nodes Become Invalid
==========================================================

Description
-----------

The system checks whether the trust relationship between the active OMS node and other Agent nodes is normal every hour. The alarm is generated if the mutual trust fails. This alarm is automatically cleared if this problem is resolved.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12066    Major          Yes
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

Some operations on the management plane may be abnormal.

Possible Causes
---------------

-  The **/etc/ssh/sshd_config** configuration file is damaged.
-  The password of user **omm** has expired.

Procedure
---------

**Check the status of the /etc/ssh/sshd_config configuration file.**

#. In the alarm list on FusionInsight Manager, locate the row that contains the alarm and click |image1| to view the host list in the alarm details.

#. Log in to the active OMS node as user **omm**.

#. Run the **ssh** command, for example, **ssh** **host2**, on each node in the alarm details to check whether the connection fails. (**host2** is a node other than the OMS node in the alarm details.)

   -  If yes, go to :ref:`4 <alm-12066__li176321676280>`.
   -  If no, go to :ref:`6 <alm-12066__li9148131091317>`.

#. .. _alm-12066__li176321676280:

   Open the **/etc/ssh/sshd_config** configuration file on host2 and check whether **AllowUsers** or **DenyUsers** is configured for other nodes.

   -  If yes, go to :ref:`5 <alm-12066__li846318425575>`.
   -  If no, contact OS experts.

#. .. _alm-12066__li846318425575:

   Modify the whitelist or blacklist to ensure that user **omm** is in the whitelist or not in the blacklist. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12066__li9148131091317>`.

**Check the status of the password of user omm.**

6. .. _alm-12066__li9148131091317:

   Check the interaction information of the **ssh** command.

   -  If the password of user **omm** is required, go to :ref:`7 <alm-12066__li81482101138>`.
   -  If message "Enter passphrase for key '/home/omm/.ssh/id_rsa':" is displayed, go to :ref:`9 <alm-12066__li106306742813>`.

7. .. _alm-12066__li81482101138:

   Check the trust list (**/home/omm/.ssh/authorized_keys**) of user **omm** on the OMS node and host2 node. Check whether the trust list contains the public key file (**/home/omm/.ssh/id_rsa.pub**) of user **omm** on the peer host.

   -  If yes, contact OS experts.
   -  If no, add the public key of user **omm** of the peer host to the trust list of the local host.

8. Add the public key of user **omm** of the peer host to the trust list of the local host. Run the **ssh** command, for example, **ssh host2**, on each node in the alarm details to check whether the connection fails. (**host2** is a node other than the OMS node in the alarm details.)

   -  If yes, go to :ref:`9 <alm-12066__li106306742813>`.
   -  If no, check whether the alarm is cleared. If the alarm is cleared, no further action is required; otherwise, go to :ref:`9 <alm-12066__li106306742813>`.

**Collect the fault information.**

9.  .. _alm-12066__li106306742813:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

10. Select **Controller** for **Service** and click **OK**.

11. Click |image2| in the upper right corner to set the log collection time range. Generally, the time range is 10 minutes before and after the alarm generation time. Click **Download**.

12. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

Perform the following steps to handle abnormal trust relationships between nodes:

.. important::

   -  Perform this operation as user **omm**.
   -  If the network between nodes is disconnected, rectify the network fault first. Check whether the two nodes are connected to the same security group and whether **hosts.deny** and **hosts.allow** are set.

#. Run the **ssh-add -l** command on both nodes to check whether any identities exist.

   |image3|

   -  If yes, go to :ref:`4 <alm-12066__li09782325586>`.
   -  If no, go to :ref:`2 <alm-12066__li16978123275815>`.

#. .. _alm-12066__li16978123275815:

   If no identities are displayed, run the **ps -ef|grep ssh-agent** command to find the **ssh-agent** process, stop the process, and wait for the process to automatically restart.

   |image4|

#. Run the **ssh-add -l** command to check whether the identities have been added. If yes, manually run the **ssh** command to check whether the trust relationship is normal.

   |image5|

#. .. _alm-12066__li09782325586:

   If identities exist, check whether the **/home/omm/.ssh/authorized_keys** file contains the information in the **/home/omm/.ssh/id_rsa.pub** file of the peer node. If it does not, manually add the information.

#. Check whether the permissions on the files in the **/home/omm/.ssh** directory are modified.

#. Check the **/var/log/Bigdata/nodeagent/scriptlog/ssh-agent-monitor.log** file.

#. If the **/home** directory of user **omm** is deleted, contact MRS support personnel for assistance.

.. |image1| image:: /_static/images/en-us_image_0263895789.png
.. |image2| image:: /_static/images/en-us_image_0263895540.png
.. |image3| image:: /_static/images/en-us_image_0000001226576418.png
.. |image4| image:: /_static/images/en-us_image_0000001227056330.png
.. |image5| image:: /_static/images/en-us_image_0000001271536445.png
