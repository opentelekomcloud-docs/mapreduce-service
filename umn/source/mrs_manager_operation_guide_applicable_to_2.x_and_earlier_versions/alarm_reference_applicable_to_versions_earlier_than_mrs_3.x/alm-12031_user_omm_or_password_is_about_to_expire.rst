:original_name: alm_12031.html

.. _alm_12031:

ALM-12031 User omm or Password Is About to Expire
=================================================

Description
-----------

The system starts at 00:00 every day to check whether user **omm** and the password are about to expire every eight hours. This alarm is generated if the user or password is about to expire in 15 days.

The alarm is cleared when the validity period of user **omm** is changed or the password is reset and the alarm handling is complete.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12031    Major          Yes
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

The node trust relationship is unavailable and Manager cannot manage the services.

Possible Causes
---------------

User **omm** or the password is about to expire.

Procedure
---------

#. Check whether user **omm** and the password in the system are valid.

   a. Log in to the faulty node.

   b. Run the following command to view the information about user **omm** and the password:

      **chage -l omm**

   c. Check whether the user has expired based on the system message.

      #. View the value of **Password expires** to check whether the password is about to expire.
      #. View the value of **Account expires** to check whether the user is about to expire.

      .. note::

         If the parameter value is **never**, the user and password are valid permanently; if the value is a date, check whether the user and password are about to expire within 15 days.

      -  If yes, go to :ref:`1.d <alm_12031__en-us_topic_0191813902_li2310249112814>`.
      -  If no, go to :ref:`2 <alm_12031__en-us_topic_0191813902_li572522141314>`.

   d. .. _alm_12031__en-us_topic_0191813902_li2310249112814:

      Run the following command to modify the validity period configuration:

      -  Run the following command to set a validity period for user **omm**:

         **chage -E** *'specified date'* **omm**

      -  Run the following command to set the number of validity days for user **omm**:

         **chage -M** *'number of days'* **omm**

   e. Check whether the alarm is cleared automatically in the next periodic check.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_12031__en-us_topic_0191813902_li572522141314>`.

#. .. _alm_12031__en-us_topic_0191813902_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

**Reference**
-------------

None
