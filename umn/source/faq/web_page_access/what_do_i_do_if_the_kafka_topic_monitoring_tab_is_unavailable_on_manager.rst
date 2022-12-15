:original_name: mrs_03_1166.html

.. _mrs_03_1166:

What Do I Do If the Kafka Topic Monitoring Tab Is Unavailable on Manager?
=========================================================================

#. Log in to each Master node of the cluster and switch to user **omm**.

#. Go to the **/opt/Bigdata/apache-tomcat-7.0.78/webapps/web/WEB-INF/lib/components/Kafka/** directory.

#. Run the **cp /opt/share/zookeeper-3.5.1-mrs-2.0/zookeeper-3.5.1-mrs-2.0.jar ./** command to copy the ZooKeeper package.

#. Restart the Tomcat process.

   **sh /opt/Bigdata/apache-tomcat-7.0.78/bin/shutdown.sh**

   **sh /opt/Bigdata/apache-tomcat-7.0.78/bin/startup.sh**
