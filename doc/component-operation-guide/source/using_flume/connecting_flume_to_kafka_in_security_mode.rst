:original_name: mrs_01_1071.html

.. _mrs_01_1071:

Connecting Flume to Kafka in Security Mode
==========================================

Scenario
--------

This section describes how to connect to Kafka using the Flume client in security mode.

This section applies to MRS 3.\ *x* or later.

Procedure
---------

#. Create a **jaas.conf** file and save it to **${**\ *Flume client installation directory*\ **} /conf**. The content of the **jaas.conf** file is as follows:

   .. code-block::

      KafkaClient {
      com.sun.security.auth.module.Krb5LoginModule required
      useKeyTab=true
      keyTab="/opt/test/conf/user.keytab"
      principal="flume_hdfs@<System domain name>"
      useTicketCache=false
      storeKey=true
      debug=true;
       };

   Set **keyTab** and **principal** based on site requirements. The configured **principal** must have certain kafka permissions.

#. Configure services. Set the port number of **kafka.bootstrap.servers** to **21007**, and set **kafka.security.protocol** to **SASL_PLAINTEXT**.

#. If the domain name of the cluster where Kafka is located is changed, change the value of *-Dkerberos.domain.name* in the **flume-env.sh** file in **$**\ {*Flume client installation directory*} **/conf/** based on the site requirements.

#. Upload the configured **properties.properties** file to **$**\ {*Flume client installation directory*} **/conf**.
