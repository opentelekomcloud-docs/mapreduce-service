:original_name: ALM-25005.html

.. _ALM-25005:

ALM-25005 nscd Service Exception
================================

Description
-----------

The system checks the status of the nscd service every 60 seconds. This alarm is generated when the nscd process fails to be queried for four consecutive times (three minutes) or users in LdapServer cannot be obtained.

This alarm is cleared when the process is restored and users in LdapServer can be obtained.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
25005    Major          Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
HostName    Host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

The alarmed node may not be able to synchronize data from LdapServer. The **id** command may fail to obtain the LDAP data, affecting upper-layer services.

Possible Causes
---------------

-  The nscd service is not started.
-  The network is faulty, and cannot access the LDAP server.
-  NameService is abnormal.
-  Users cannot be queried because the OS executes commands too slowly.

Procedure
---------

**Check whether the nscd service is started.**

#. Log in to FusionInsight Manager and choose **O&M** > **Alarm** > **Alarms**. Record the IP address of **HostName** in **Location** of the alarm as **IP1** (if multiple alarms exist, record the IP addresses as **IP1**, **IP2**, and **IP3** respectively).

#. Contact the O&M personnel to access the node using IP1 as user **root**. Run the **ps -ef \| grep nscd** command on the node and check whether the **/usr/sbin/nscd** process is started.

   -  If yes, go to :ref:`5 <alm-25005__li423153448513>`.
   -  If no, go to :ref:`3 <alm-25005__li600689958513>`.

#. .. _alm-25005__li600689958513:

   Run the **service nscd restart** command as user **root** to restart the nscd service. Then run the **ps -ef \| grep nscd** command to check whether the nscd service is started.

   -  If yes, go to :ref:`4 <alm-25005__li67767558513>`.
   -  If no, go to :ref:`15 <alm-25005__li265529978513>`.

#. .. _alm-25005__li67767558513:

   Wait for 5 minutes and run the ps -ef \| grep nscd command again as user root. Check whether the service exists.

   -  If yes, go to :ref:`11 <alm-25005__li551461168513>`.
   -  If no, go to :ref:`15 <alm-25005__li265529978513>`.

**Check whether the network is faulty, and whether the LDAP server can be accessed.**

5. .. _alm-25005__li423153448513:

   Log in to the alarmed node as user **root** and run the **ping** command to check whether the network connectivity between this node and the LdapServer node. is normal.

   -  If yes, go to :ref:`6 <alm-25005__li297764118513>`.
   -  If no, contact network administrators to troubleshoot the fault.

**Check whether the NameService is normal.**

6.  .. _alm-25005__li297764118513:

    Log in to the alarmed node as user **root**. Run the **cat /etc/nsswitch.conf** command to check whether the **passwd**, **group**, **services**, **netgroup**, and **aliases** of NameService are correctly configured.

    The correct parameter configurations are as follows:

    **passwd**: **compat ldap**; **group**: **compat ldap**; **services**: **files ldap**; **netgroup**: **files ldap**; **aliases**: **files ldap**

    -  If yes, go to :ref:`7 <alm-25005__li11806553308>`.
    -  If no, go to :ref:`9 <alm-25005__li195824098513>`.

7.  .. _alm-25005__li11806553308:

    Log in to the alarmed node as user **root**. Run the **cat /etc/nscd.conf** command to check whether the **enable-cache passwd**, **positive-time-to-live passwd**, **enable-cache group**, and **positive-time-to-live group** in the configuration file are correctly configured.

    The correct parameter configurations are as follows:

    **enable-cache passwd**: **yes**; **positive-time-to-live passwd**: **600**; **enable-cache group**: **yes**; **positive-time-to-live group**: **3600**

    -  If yes, go to :ref:`8 <alm-25005__li389947948513>`.
    -  If no, go to :ref:`10 <alm-25005__li1648032715218>`.

8.  .. _alm-25005__li389947948513:

    Run the **/usr/sbin/nscd -i group** and **/usr/sbin/nscd -i passwd** commands as user **root**. Wait for 2 minutes and run the **id admin** and **id backup/manager** commands to check whether results can be queried.

    -  If yes, go to :ref:`11 <alm-25005__li551461168513>`.
    -  If no, go to :ref:`15 <alm-25005__li265529978513>`.

9.  .. _alm-25005__li195824098513:

    Run the **vi /etc/nsswitch.conf** command as user **root**. Correct the configurations in :ref:`6 <alm-25005__li297764118513>` and save the file. Run the **service nscd restart** command to restart the nscd service. Wait for 2 minutes and run the **id admin** and **id backup/manager** commands to check whether results can be queried.

    -  If yes, go to :ref:`11 <alm-25005__li551461168513>`.
    -  If no, go to :ref:`15 <alm-25005__li265529978513>`.

10. .. _alm-25005__li1648032715218:

    Run the **vi /etc/nscd.conf** command as user **root**. Correct the configurations in :ref:`7 <alm-25005__li11806553308>` and save the file. Run the **service nscd restart** command to restart the nscd service. Wait for 2 minutes and run the **id admin** and **id backup/manager** commands to check whether results can be queried.

    -  If yes, go to :ref:`11 <alm-25005__li551461168513>`.
    -  If no, go to :ref:`15 <alm-25005__li265529978513>`.

11. .. _alm-25005__li551461168513:

    Log in to the FusionInsight Manager portal. Wait for 5 minutes and check whether the **nscd Service Exception** alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-25005__li1693832195142>`.

**Check whether frame freezing occurs when running a command in the operating system.**

12. .. _alm-25005__li1693832195142:

    Log in to the faulty node as user **root**, run the **id admin** command, and check whether the command execution takes a long time. If the command execution takes more than 3 seconds, the command execution is deemed to be slow.

    -  If yes, go to :ref:`13 <alm-25005__li97084049527>`.
    -  If no, go to :ref:`15 <alm-25005__li265529978513>`.

13. .. _alm-25005__li97084049527:

    Run the **cat /var/log/messages** command to check whether the nscd frequently restarts or the error information "Can't contact LDAP server" exists.

    nscd exception example:

    .. code-block::

       Feb 11 11:44:42 10-120-205-33 nscd: nss_ldap: failed to bind to LDAP server ldaps://10.120.205.55:21780: Can't contact LDAP server
       Feb 11 11:44:43 10-120-205-33 ntpq: nss_ldap: failed to bind to LDAP server ldaps://10.120.205.55:21780: Can't contact LDAP server
       Feb 11 11:44:44 10-120-205-33 ntpq: nss_ldap: failed to bind to LDAP server ldaps://10.120.205.92:21780: Can't contact LDAP server

    -  If yes, go to :ref:`14 <alm-25005__li3335145595227>`.
    -  If no, go to :ref:`15 <alm-25005__li265529978513>`.

14. .. _alm-25005__li3335145595227:

    Run the **vi$BIGDATA_HOME/tmp/random_ldap_ip_order** command to modify the number at the end. If the original number is an odd number, change it to an even number. If the number is an even number, change it to an odd number.

    Run the **vi /etc/ldap.conf** command to enter the editing mode, press **Insert** to start editing, and then change the first two IP addresses of the URI configuration item.

    After the modification is complete, press **Esc** to exit the editing mode and enter **:wq!** to save the settings and exit.

    Run the **service nscd restart** command to restart the nscd service. Wait 5 minutes and run the **id admin** command again. Check whether the command execution is slow.

    -  If yes, go to :ref:`15 <alm-25005__li265529978513>`.
    -  If no, log in to other faulty nodes and repeat :ref:`12 <alm-25005__li1693832195142>` to :ref:`14 <alm-25005__li3335145595227>` to check whether the first LdapServer node in the URI before modifying **/etc/ldap.conf** is faulty. For example, check whether the service IP address is unreachable, the network delay is too long, or other abnormal software is deployed.

**Collect the fault information.**

15. .. _alm-25005__li265529978513:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

16. Expand the drop-down list next to the **Service** field. In the **Services** dialog box that is displayed, select **LdapClient** for the target cluster.

17. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

18. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0263895532.png
