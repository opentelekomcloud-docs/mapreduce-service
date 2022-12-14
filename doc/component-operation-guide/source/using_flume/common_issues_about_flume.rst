:original_name: mrs_01_1598.html

.. _mrs_01_1598:

Common Issues About Flume
=========================

Flume logs are stored in **/var/log/Bigdata/flume/flume/flumeServer.log**. Most data transmission exceptions and data transmission failures are recorded in logs. You can run the following command:

**tailf /var/log/Bigdata/flume/flume/flumeServer.log**

-  Problem: After the configuration file is uploaded, an exception occurs. After the configuration file is uploaded again, the scenario requirements are still not met, but no exception is recorded in the log.

   Solution: Restart the Flume process, run the **kill -9** *Process code* to kill the process code, and view the logs.

-  Issue: **"java.lang.IllegalArgumentException: Keytab is not a readable file: /opt/test/conf/user.keytab"** is displayed when HDFS is connected.

   Solution: Grant the read and write permissions to the Flume running user.

-  Problem: The following error is reported when the Flume client is connected to Kafka:

   .. code-block::

      Caused by: java.io.IOException: /opt/FlumeClient/fusioninsight-flume-1.9.0/cof//jaas.conf (No such file or directory)

   Solution: Add the **jaas.conf** configuration file and save it to the **conf** directory of the Flume client.

   **vi jaas.conf**

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

   Values of **keyTab** and **principal** vary depending on the actual situation.

-  Problem: The following error is reported when the Flume client is connected to HBase:

   .. code-block::

      Caused by: java.io.IOException: /opt/FlumeClient/fusioninsight-flume-1.9.0/cof//jaas.conf (No such file or directory)

   Solution: Add the **jaas.conf** configuration file and save it to the **conf** directory of the Flume client.

   **vi jaas.conf**

   .. code-block::

      Client {
      com.sun.security.auth.module.Krb5LoginModule required
      useKeyTab=true
      keyTab="/opt/test/conf/user.keytab"
      principal="flume_hbase@<System domain name>"
      useTicketCache=false
      storeKey=true
      debug=true;
      };

   Values of **keyTab** and **principal** vary depending on the actual situation.

-  Question: After the configuration file is submitted, the Flume Agent occupies resources. How do I restore the Flume Agent to the state when the configuration file is not uploaded?

   Solution: Submit an empty **properties.properties** file.
