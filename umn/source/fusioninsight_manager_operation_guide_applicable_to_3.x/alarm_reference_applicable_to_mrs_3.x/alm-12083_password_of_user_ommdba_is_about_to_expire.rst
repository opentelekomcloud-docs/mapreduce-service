:original_name: ALM-12083.html

.. _ALM-12083:

ALM-12083 Password of User ommdba Is About to Expire
====================================================

Description
-----------

The system starts at 00:00 every day to check whether the password of user **ommdba** is about to expire every 8 hours. This alarm is generated if the password is about to expire no less than 15 days later.

This alarm is cleared when the expiration time of user **ommdba** password is reset and the user password status becomes normal.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12083    Minor          Yes
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

The OMS database cannot be managed and data cannot be accessed.

Possible Causes
---------------

The password of user **ommdba** is about to expire.

Procedure
---------

**Check whether the password of user ommdba in the system is about to expire.**

#. Log in to the faulty node as user **root**.

   Run the **chage -l ommdba** command to view the information about the password of user **ommdba**.

#. View the value of **Password expires** to check whether the user configurations are about to expire.

   .. note::

      If the parameter value is **never**, the user and password are valid permanently; if the value is a date, check whether the user and password are about to expire within 15 days.

   -  If they are, go to :ref:`3 <alm-12083__li181858713577>`.
   -  If they are not, go to :ref:`4 <alm-12083__li51831473571>`.

#. .. _alm-12083__li181858713577:

   Run the **chage -M** *'days*\ **' ommdba** command to set the validity period of the password for user **ommdba**. Eight hours later, check whether the alarm is automatically cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`4 <alm-12083__li51831473571>`.

**Collect fault information.**

4. .. _alm-12083__li51831473571:

   On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

5. Select **NodeAgent** for **Service** and click **OK**.

6. Click |image1| in the upper right corner. In the displayed dialog box, set **Start Date** and **End Date** to 10 minutes before and after the alarm generation time respectively and click **OK**. Then, click **Download**.

7. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

This alarm will be automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532607974.png
