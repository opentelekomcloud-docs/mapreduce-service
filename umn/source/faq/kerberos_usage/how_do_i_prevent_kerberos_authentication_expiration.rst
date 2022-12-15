:original_name: mrs_03_1167.html

.. _mrs_03_1167:

How Do I Prevent Kerberos Authentication Expiration?
====================================================

-  Java applications:

   Before connecting to HBase, HDFS, or other big data components, call loginUserFromKeytab() to create a UGI. Then, start a scheduled thread to periodically check whether the Kerberos Authentication expires. Log in to the system again before the Kerberos Authentication expires.

   .. code-block::

      private static void startCheckKeytabTgtAndReloginJob() {
      //The credential is checked every 10 minutes, and updated before the expiration time.
              ThreadPool.updateConfigThread.scheduleWithFixedDelay(() -> {
                  try {
                      UserGroupInformation.getLoginUser().checkTGTAndReloginFromKeytab();
                      logger.warn("get tgt:{}", UserGroupInformation.getLoginUser().getTGT());
                      logger.warn("Check Kerberos Tgt And Relogin From Keytab Finish.");
                  } catch (IOException e) {
                      logger.error("Check Kerberos Tgt And Relogin From Keytab Error", e);
                  }
              }, 0, 10, TimeUnit.MINUTES);
              logger.warn("Start Check Keytab TGT And Relogin Job Success.");
          }

-  Tasks executed in shell mode:

   #. Run the **kinit** command to authenticate the user.
   #. Create a scheduled task of the operating system or any other scheduled task to run the **kinit** command to authenticate the user periodically.
   #. Submit jobs to execute big data tasks.

-  Spark jobs:

   If you submit jobs using spark-shell, spark-submit, or spark-sql, you can specify **Keytab** and **Principal** in the command to perform authentication and periodically update the login credential and authorization tokens to prevent authentication expiration.

   Example:

   **spark-shell --principal spark2x/hadoop.**\ <*System domain name*>@<*System domain name*>\ ** --keytab ${BIGDATA_HOME}/FusionInsight_Spark2x_8.1.0.1/install/FusionInsight-Spark2x-2.4.5/keytab/spark2x/SparkResource/spark2x.keytab --master yarn**
