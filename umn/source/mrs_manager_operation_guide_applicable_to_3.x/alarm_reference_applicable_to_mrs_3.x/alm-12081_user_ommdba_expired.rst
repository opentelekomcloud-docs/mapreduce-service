:original_name: ALM-12081.html

.. _ALM-12081:

ALM-12081 User ommdba Expired
=============================

Description
-----------

The system starts at 00:00 every day to check whether user **ommdba** has expired every 8 hours. This alarm is generated if the user account has expired.

This alarm is cleared when the expiration time of user **ommdba** is reset and the user account status becomes normal.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12081    Major          Yes
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

The account of user **ommdba** for the host has expired.

Procedure
---------

**Check whether user ommdba has expired.**

#. Log in to the faulty node as user **root**.

   Run the **chage -l ommdba** command to view the information about the password of user **ommdba**.

#. View the value of **Account expires** to check whether the user configurations have expired.

   .. note::

      If the parameter value is **never**, the user and password are valid permanently; if the value is a date, check whether the user and password have expired.

   -  If they do, go to :ref:`3 <alm-12081__li1254561011>`.
   -  If they do not, go to :ref:`4 <alm-12081__li65317618114>`.

#. .. _alm-12081__li1254561011:

   Run the **chage -E** *'yyyy-MM-dd'* **omm** command to set the validity period of user **ommdba**. Eight hours later, check whether the alarm is automatically cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`4 <alm-12081__li65317618114>`.

**Collect fault information.**

4. .. _alm-12081__li65317618114:

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

.. |image1| image:: /_static/images/en-us_image_0000001582807877.png
