:original_name: mrs_01_1047.html

.. _mrs_01_1047:

Configuring a Storm Service User Password Policy
================================================

Scenario
--------

This section applies to MRS 3.\ *x* or later.

After submitting a topology task, a Storm service user must ensure that the task continuously runs. During topology running, the worker process may need to restart to ensure continuous topology work. If the password of a service user is changed or the number of days that a password is used exceeds the maximum number specified in a password policy, topology running may be affected. A system administrator must configure a separate password policy for Storm service users based on enterprise security requirements.

.. note::

   If a separate password policy is not configured for Storm service users, an old topology can be deleted and then submitted again after a service user password is changed so that the topology can continuous run.

Impact on the System
--------------------

-  After a separate password policy is configured for a Storm service user, the user is not affected by **Password Policy** on the Manager page.
-  If a separate password policy is configured for a Storm service user and cross-cluster entrusted relationships are configured, a password must be reset for the Storm service user on Manager based on the password policy.

Prerequisites
-------------

A system administrator has understood service requirements and created a **Human-Machine** user, for example, **testpol**.

Procedure
---------

#. Log in to any node in the cluster as user **omm**.

#. Run the following command to disable logout upon timeout:

   **TMOUT=0**

   .. note::

      After the operations in this section are complete, run the **TMOUT=**\ *Timeout interval* command to restore the timeout interval in a timely manner. For example, **TMOUT=600** indicates that a user is logged out if the user does not perform any operation within 600 seconds.

#. Run the following commands to export the environment variables:

   **EXECUTABLE_HOME="${CONTROLLER_HOME}/kerberos_user_specific_binay/kerberos"**

   **LD_LIBRARY_PATH=${EXECUTABLE_HOME}/lib:$LD_LIBRARY_PATH**

   **PATH=${EXECUTABLE_HOME}/bin:$PATH**

#. Run the following command and enter the Kerberos administrator password to log in to the Kerberos console:

   **kadmin -p kadmin/admin**

   .. note::

      For initial use, the **kadmin/admin** password must be changed for the **kadmin/admin** user.

   If the following information is displayed, you have successfully logged in to the Kerberos console.

   .. code-block::

      kadmin:

#. Run the following command to check details about the created **Human-Machine** user:

   **getprinc**\ *Username*

   Sample command for viewing details about the **testpol** user:

   **getprinc testpol**

   If the following information is displayed, the specified user has used the default password policy:

   .. code-block::

      Principal: testpol@<System domain name>
      ......
      Policy: default

#. Run the following command to create a separate password policy, such as **streampol**, for the Storm service user:

   **addpol -maxlife 0day -minlife 0sec -history 1 -maxfailure 5 -failurecountinterval 5min -lockoutduration 5min -minlength 8 -minclasses 4 streampol**

   In the command, **-maxlife** indicates the maximum validity period of a password, and **0day** indicates that a password will never expire.

#. Run the following command to view the newly created policy **streampol**:

   **getpol streampol**

   If the following information is displayed, the new policy specifies that the password will never expire:

   .. code-block::

      Policy: streampol
       Maximum password life: 0 days 00:00:00
      ......

#. Run the following command to apply the new policy **streampol** to the **testpol** Storm user:

   **modprinc -policy streampol testpol**

   In the command, **streampol** indicates a policy name, and **testpol** indicates a username.

   If the following information is displayed, the properties of the specified user have been modified:

   .. code-block::

      Principal "testpol@<System domain name>" modified.

#. Run the following command to view current information about the **testpol** Storm user:

   **getprinc testpol**

   If the following information is displayed, the specified user has used the new password policy:

   .. code-block::

      Principal: testpol@<System domain name>
      ......
       Policy: streampol
