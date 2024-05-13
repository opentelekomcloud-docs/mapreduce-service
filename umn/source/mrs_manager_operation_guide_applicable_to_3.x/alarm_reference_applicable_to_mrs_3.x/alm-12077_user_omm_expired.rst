:original_name: ALM-12077.html

.. _ALM-12077:

ALM-12077 User omm Expired
==========================

Description
-----------

The system starts at 00:00 every day to check whether user **omm** has expired every eight hours. This alarm is generated if the user account has expired.

This alarm is cleared when the expiration time of user **omm** is changed and the user account status becomes normal.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12077    Major          Yes
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

User **omm** has expired. The node trust relationship is unavailable, and MRS Manager cannot manage the services.

Possible Causes
---------------

User **omm** has expired.

Procedure
---------

**Check whether user omm in the system has expired.**

#. Log in to the faulty node as user **root**.

   Run the **chage -l omm**\ command to view the information about the password of user **omm**.

#. View the value of **Account expires** to check whether the user configurations have expired.

   .. note::

      If the parameter value is **never**, the user configurations never expire.

   -  If they do, go to :ref:`3 <alm-12077__li20789183613915>`.
   -  If they do not, go to :ref:`4 <alm-12077__li877819366912>`.

#. .. _alm-12077__li20789183613915:

   Run the **chage -E 'yyyy-MM-dd' omm** command to set the expiration time of user **omm**. Eight hours later, check whether the alarm is automatically cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`4 <alm-12077__li877819366912>`.

**Collect fault information.**

4. .. _alm-12077__li877819366912:

   On MRS Manager, choose **O&M** > **Log** > **Download**.

5. Select **NodeAgent** for **Service** and click **OK**.

6. Click |image1| in the upper right corner. In the displayed dialog box, set **Start Date** and **End Date** to 10 minutes before and after the alarm generation time respectively and click **OK**. Then, click **Download**.

7. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

This alarm will be automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807821.png
