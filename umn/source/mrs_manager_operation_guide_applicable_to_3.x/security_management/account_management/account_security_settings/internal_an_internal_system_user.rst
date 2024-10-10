:original_name: admin_guide_000246.html

.. _admin_guide_000246:

Internal an Internal System User
================================

Scenario
--------

If the service is abnormal, the internal user of the system may be locked. Unlock the user promptly, or the cluster cannot run properly. For the list of system internal users, see :ref:`User Account List <admin_guide_000239>` in . The internal user of the system cannot be unlocked using MRS Manager.

Prerequisites
-------------

Obtain the default password of the LDAP administrator **cn=root,dc=hadoop,dc=com** by referring to :ref:`User Account List <admin_guide_000239>` in .

Procedure
---------

#. Use the following method to confirm whether the internal system username is locked:

   a. OLdap port number obtaining method:

      #. Log in to MRS Manager, choose **System** > **OMS** > **oldap** > **Modify Configuration**.
      #. The **LDAP Listening Port** parameter value is **oldap port**.

   b. Domain name obtaining method:

      #. Log in to MRS Manager, choose **System** > **Permission** > **Domain and Mutual Trust**.

      #. The **Local Domain** parameter value is the domain name.

         For example, the domain name of the current system is **9427068F-6EFA-4833-B43E-60CB641E5B6C.COM**.

   c. Run the following command on each node in the cluster as user **omm** to query the number of password authentication failures:

      **ldapsearch -H ldaps://**\ *OMS Floating IP Address*\ **:**\ *OLdap port* **-LLL -x -D cn=root,dc=hadoop,dc=com -b krbPrincipalName=**\ *Internal system username*\ **@**\ *Domain name*\ **,cn=**\ *Domain name*\ **,cn=krbcontainer,dc=hadoop,dc=com -w** *Password of LDAP administrator* **-e ppolicy \| grep krbLoginFailedCount**

      For example, run the following command to check the number of password authentication failures for user **oms/manager**:

      **ldapsearch -H ldaps://10.5.146.118:21750 -LLL -x -D cn=root,dc=hadoop,dc=com -b krbPrincipalName=oms/manager@9427068F-6EFA-4833-B43E-60CB641E5B6C.COM,cn=9427068F-6EFA-4833-B43E-60CB641E5B6C.COM,cn=krbcontainer,dc=hadoop,dc=com -w** *Password of user cn=root,dc=hadoop,dc=com* **-e ppolicy \| grep krbLoginFailedCount**

      .. code-block::

         krbLoginFailedCount: 5

   d. Log in to MRS Manager, choose **System** > **Permission** > **Security Policy** > **Password Policy**.

   e. Check the value of the **Password Retries** parameter. If the value is less than or equal to the value of **krbLoginFailedCount**, the user is locked.

      .. note::

         You can also check whether internal users are locked by viewing operations logs.

#. Log in to the active management node as user **omm** and run the following command to unlock the user:

   **sh ${BIGDATA_HOME}/om-server/om/share/om/acs/config/unlockuser.sh --userName** *Internal system username*

   Example: **sh ${BIGDATA_HOME}/om-server/om/share/om/acs/config/unlockuser.sh --userName oms/manager**
