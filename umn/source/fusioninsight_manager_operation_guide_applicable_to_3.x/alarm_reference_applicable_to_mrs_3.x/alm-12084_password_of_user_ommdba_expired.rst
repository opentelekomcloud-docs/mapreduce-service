:original_name: ALM-12084.html

.. _ALM-12084:

ALM-12084 Password of User ommdba Expired
=========================================

Description
-----------

The system starts at 00:00 every day to check whether the password of user **ommdba** has expired every 8 hours. This alarm is generated if the password has expired.

This alarm is cleared when the expiration time of user **ommdba** password is reset and the user password status becomes normal.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12084    Major          Yes
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

The password of user **ommdba** has expired. The node trust relationship is unavailable, and FusionInsight Manager cannot manage the services.

Possible Causes
---------------

The password of user **ommdba** for the host has expired.

Procedure
---------

**Check whether the password of user ommdba in the system has expired.**

#. Log in to the faulty node as user **root**.

   Run the **chage -l ommdba** command to view the information about the password of user **ommdba**.

#. View the value of **Password expires** to check whether the user configurations have expired.

   .. note::

      If the parameter value is **never**, the user and password are valid permanently; if the value is a date, check whether the user and password have expired.

   -  If they do, go to :ref:`3 <alm-12084__li6810122017542>`.
   -  If they do not, go to :ref:`4 <alm-12084__li2808420175418>`.

#. .. _alm-12084__li6810122017542:

   Run the **chage -M** *'days*\ **' ommdba** command to set the validity period of the password for user **ommdba**. Eight hours later, check whether the alarm is automatically cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`4 <alm-12084__li2808420175418>`.

**Collect fault information.**

4. .. _alm-12084__li2808420175418:

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

.. |image1| image:: /_static/images/en-us_image_0269383930.png
