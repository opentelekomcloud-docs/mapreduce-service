:original_name: mrs_01_2317.html

.. _mrs_01_2317:

Adapting to the Third-party JDK When Ranger Is Used
===================================================

Scenarios
---------

When Ranger is used as the permission management service of Spark SQL, the certificate in the cluster is required for accessing RangerAdmin. If you use a third-party JDK instead of the JDK or JRE in the cluster, RangerAdmin fails to be accessed. As a result, the Spark application fails to be started.

In this scenario, you need to perform the following operations to import the certificate in the cluster to the third-party JDK or JRE.

Configuration Method
--------------------

#. .. _mrs_01_2317__en-us_topic_0000001219350557_li1868718267616:

   Run the following command to export the certificate from the cluster:

   a. Install the cluster client. Assume that the installation path is **/opt/client**.

   b. Run the following command to go to the client installation directory.

      **cd /opt/client**

   c. Run the following command to configure environment variables:

      **source bigdata_env**

   d. Generate the certificate file.

      **keytool -export -alias fusioninsightsubroot -storepass changeit -keystore /opt/client/JRE/jre/lib/security/cacerts -file fusioninsightsubroot.crt**

#. Import the certificate in the cluster to the third-party JDK or JRE.

   Copy the **fusioninsightsubroot.crt** file generated in :ref:`1 <mrs_01_2317__en-us_topic_0000001219350557_li1868718267616>` to the third-party JRE node, set the **JAVA_HOME** environment variable of the node, and run the following command to import the certificate:

   **keytool -import -trustcacerts -alias fusioninsightsubroot -storepass changeit -file fusioninsightsubroot.crt -keystore MY_JRE/lib/security/cacerts**

   .. note::

      **MY_JRE** indicates the installation path of the third-party JRE. Change it based on the site requirements.
