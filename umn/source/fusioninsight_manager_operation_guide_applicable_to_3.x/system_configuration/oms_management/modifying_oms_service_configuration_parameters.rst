:original_name: admin_guide_000162.html

.. _admin_guide_000162:

Modifying OMS Service Configuration Parameters
==============================================

Scenario
--------

Based on the security requirements of the user environment, you can modify the Kerberos and LDAP configurations in the OMS on FusionInsight Manager.

Impact on the System
--------------------

After the OMS service configuration parameters are modified, the corresponding OMS module needs to be restarted. In this case, FusionInsight Manager cannot be used.

Procedure
---------

**Modifying the okerberos configuration**

#. Log in to FusionInsight Manager and choose **System** > **OMS**.

2. Locate the row that contains okerberos and click **Modify Configuration**.

3. Modify the parameters according to :ref:`Table 1 <admin_guide_000162__table19796438111412>`.

   .. _admin_guide_000162__table19796438111412:

   .. table:: **Table 1** okerberos parameters

      +--------------------------+----------------------------------------------------------------------------------------------------------------+
      | Parameter                | Description                                                                                                    |
      +==========================+================================================================================================================+
      | KDC Timeout (ms)         | Timeout duration for an application to connect to Kerberos, in milliseconds. The value must be an integer.     |
      +--------------------------+----------------------------------------------------------------------------------------------------------------+
      | Max Retries              | Maximum number of retries for an application to connect to Kerberos, in seconds. The value must be an integer. |
      +--------------------------+----------------------------------------------------------------------------------------------------------------+
      | LDAP Timeout (ms)        | Timeout duration for Kerberos to connect to LDAP, in milliseconds.                                             |
      +--------------------------+----------------------------------------------------------------------------------------------------------------+
      | LDAP Search Timeout (ms) | Timeout duration for Kerberos to query user information in LDAP, in milliseconds.                              |
      +--------------------------+----------------------------------------------------------------------------------------------------------------+
      | Kadmin Listening Port    | Port number of the Kadmin service.                                                                             |
      +--------------------------+----------------------------------------------------------------------------------------------------------------+
      | KDC Listening Port       | Port number of the kinit service.                                                                              |
      +--------------------------+----------------------------------------------------------------------------------------------------------------+
      | Kpasswd Listening Port   | Port number of the Kpasswd service.                                                                            |
      +--------------------------+----------------------------------------------------------------------------------------------------------------+

4. Click **OK**.

   In the displayed dialog box, enter the password of the current login user and click **OK**. In the displayed confirmation dialog box, click **OK**.

**Modifying the oldap configuration**

5. Locate the row that contains the oldap and click **Modify Configuration**.

6. Modify the parameters according to :ref:`Table 2 <admin_guide_000162__table1696932817285>`.

   .. _admin_guide_000162__table1696932817285:

   .. table:: **Table 2** OLDAP parameters

      =================== ================================
      Parameter           Description
      =================== ================================
      LDAP Listening Port Port number of the LDAP service.
      =================== ================================

7. Click **OK**.

   In the displayed dialog box, enter the password of the current login user and click **OK**. In the displayed confirmation dialog box, click **OK**.

   .. note::

      To reset the password of the LDAP account, you need to restart ACS. The procedure is as follows:

      a. Log in to the active management node as user **omm** using PuTTY, and run the following command to update the domain configuration:

         **sh ${BIGDATA_HOME}/om-server/om/sbin/restart-RealmConfig.sh**

         The command is run successfully if the following information is displayed:

         .. code-block::

            Modify realm successfully. Use the new password to log into FusionInsight again.

      b. Run the **sh $CONTROLLER_HOME/sbin/acs_cmd.sh stop** command to stop ACS.

      c. Run the **sh $CONTROLLER_HOME/sbin/acs_cmd.sh start** command to start ACS.

**Restarting the cluster**

8. Log in to FusionInsight Manager and restart the cluster by referring to :ref:`Performing a Rolling Restart of a Cluster <admin_guide_000012>`.
