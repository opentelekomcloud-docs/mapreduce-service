:original_name: mrs_03_1113.html

.. _mrs_03_1113:

How Do I Balance HDFS Data?
===========================

#. Log in to the master node of the cluster and run the corresponding command to configure environment variables. **/opt/client** indicates the client installation directory. Replace it with the actual one.

   **source /opt/client/bigdata_env**

   **kinit** **Component service user** (If Kerberos authentication is enabled for the cluster, run this command to authenticate the user. Skip this step if the Kerberos authentication is disabled.)

#. Run the following command to start the balancer:

   **/opt/client/HDFS/hadoop/sbin/start-balancer.sh -threshold 5**

#. View the log.

   After you execute the balance task, the **hadoop-root-balancer-**\ *Host name*\ **.log** log file will be generated in the client installation directory **/opt/client/HDFS/hadoop/logs**.

#. (Optional) If you do not want to perform data balancing, run the following commands to stop the balancer:

   **source /opt/client/bigdata_env**

   **kinit** **Component service user** (If Kerberos authentication is enabled for the cluster, run this command to authenticate the user. Skip this step if the Kerberos authentication is disabled.)

   **/opt/client/HDFS/hadoop/sbin/stop-balancer.sh -threshold 5**
