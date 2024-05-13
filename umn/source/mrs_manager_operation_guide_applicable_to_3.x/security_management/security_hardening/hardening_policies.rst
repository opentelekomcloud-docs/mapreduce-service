:original_name: admin_guide_000272.html

.. _admin_guide_000272:

Hardening Policies
==================

Hardening Tomcat
----------------

Tomcat is hardened as follows based on open-source software during MRS Manager software installation and use:

-  The Tomcat version is upgraded to the official version.
-  Permissions on the directories under applications are set to **500**, and the write permission on some directories is supported.
-  The Tomcat installation package is automatically deleted after the system software is installed.
-  The automatic deployment function is disabled for projects in application directories. Only the **web**, **cas**, and **client** projects are deployed.
-  Some unused **http** methods are disabled, preventing attacks by using the **http** methods.
-  The default shutdown port and command of the Tomcat server are changed to prevent hackers from shutting down the server and attacking servers and applications.
-  To ensure security, the value of **maxHttpHeaderSize** is changed, which enables server administrators to control abnormal requests of clients.
-  The Tomcat version description file is modified after Tomcat is installed.
-  To prevent disclosure of Tomcat information, the Server attributes of Connector are modified so that attackers cannot obtain information about the server.
-  Permissions on files and directories of Tomcat, such as the configuration files, executable files, log directories, and temporary folders, are under control.
-  Session facade recycling is disabled to prevent request leakage.
-  LegacyCookieProcessor is used as CookieProcessor to prevent the leakage of sensitive data in cookies.

Hardening LDAP
--------------

LDAP is hardened as follows after a cluster is installed:

-  In the LDAP configuration file, the password of the administrator account is encrypted using SHA. After the OpenLDAP is upgraded to 2.4.39 or later, data is automatically synchronized between the active and standby LDAP nodes using the SASL External mechanism, which prevents disclosure of the password.
-  The LDAP service in the cluster supports the SSLv3 protocol by default, which can be used safely. When the OpenLDAP is upgraded to 2.4.39 or later, the LDAP automatically uses TLS1.0 or later to prevent unknown security risks.

Hardening JDK
-------------

-  If the client process uses the AES256 encryption algorithm, JDK security hardening is required. The operations are as follows:

   Obtain the Java Cryptography Extension (JCE) package whose version matches that of JDK. The JCE package contains **local_policy.jar** and **US_export_policy.jar**. Copy the JAR files to the following directory and replace the files in the directory.

   -  Linux: *JDK installation directory*\ **/jre/lib/security**
   -  Windows: *JDK installation directory*\ **\\jre\\lib\\security**

   .. note::

      Access the Open JDK open-source community to obtain the JCE file.

-  If the client process uses the SM4 encryption algorithm, the JAR package needs to be updated.

   Obtain **SMS4JA.jar** in the *client installation directory*\ **/JDK/jdk/jre/lib/ext/** directory, and copy the JAR package to the following directory:

   -  Linux: *JDK installation directory*\ **/jre/lib/ext/**
   -  Windows: *JDK installation directory*\ **\\jre\\lib\\ext\\**
