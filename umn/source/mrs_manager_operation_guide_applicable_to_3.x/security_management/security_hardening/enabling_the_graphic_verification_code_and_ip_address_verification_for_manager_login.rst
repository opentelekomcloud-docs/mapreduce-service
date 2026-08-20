:original_name: admin_guide_000431.html

.. _admin_guide_000431:

Enabling the Graphic Verification Code and IP Address Verification for Manager Login
====================================================================================

Configuring Graphic Code Verification for Login
-----------------------------------------------

CAPTCHA verification during login can be enabled for clusters of MRS 3.6.0 or later to strengthen the system's resistance to brute-force cracking attacks. After enabling this feature, each login will require verification of graphic verification code.

By default, this feature is disabled; you can manually enable it by referring to this section.

#. Log in to the active management node as user **omm**.

#. .. _admin_guide_000431__li9770134823413:

   Run the following command to modify the configuration:

   **vi ${BIGDATA_HOME}/om-server/tomcat/webapps/cas/WEB-INF/classes/config/application.properties**

   Set **cas.authn.rest.captcha-enabled** to **true**.

#. Run the following command to restart Tomcat:

   **sh ${BIGDATA_HOME}/om-server/tomcat/bin/shutdown.sh;sh ${BIGDATA_HOME}/om-server/tomcat/bin/startup.sh**

#. Log in to the standby management node as user **omm**, and perform :ref:`2 <admin_guide_000431__li9770134823413>`.

Enabling IP Address Verification for Login
------------------------------------------

IP address verification during login can be enabled for clusters of MRS 3.6.0 or later to strengthen the system's resistance to brute-force cracking attacks. After enabling this feature, the IP address will be locked for 5 minutes if login fails for five consecutive times. After 5 minutes, the account can be unlocked after a successful login; otherwise, it will remain locked.

By default, this feature is disabled; you can manually enable it by referring to this section.

#. Log in to the active management node as user **omm**.

#. .. _admin_guide_000431__li44457241334:

   Run the following command to modify the configuration:

   **vi ${BIGDATA_HOME}/om-server/tomcat/webapps/cas/WEB-INF/classes/config/application.properties**

   Set **cas.authn.rest.ip-check-enabled** to **true**.

#. Run the following command to restart Tomcat:

   **sh ${BIGDATA_HOME}/om-server/tomcat/bin/shutdown.sh;sh ${BIGDATA_HOME}/om-server/tomcat/bin/startup.sh**

#. Log in to the standby management node as user **omm**, and perform :ref:`2 <admin_guide_000431__li44457241334>`.
