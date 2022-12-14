:original_name: mrs_01_2021.html

.. _mrs_01_2021:

Why Does the Realm Information Fail to Be Obtained When SparkBench is Run on HiBench for the Cluster in Security Mode?
======================================================================================================================

Question
--------

Execution of the sparkbench task (for example, Wordcount) of HiBench6 fails. The bench.log indicates that the Yarn task fails to be executed. The failure information displayed on the Yarn UI is as follows:

.. code-block::

   Exception in thread "main" org.apache.spark.SparkException: Unable to load YARN support
     at org.apache.spark.deploy.SparkHadoopUtil$.liftedTree1$1(SparkHadoopUtil.scala:390)
     at org.apache.spark.deploy.SparkHadoopUtil$.yarn$lzycompute(SparkHadoopUtil.scala:385)
     at org.apache.spark.deploy.SparkHadoopUtil$.yarn(SparkHadoopUtil.scala:385)
     at org.apache.spark.deploy.SparkHadoopUtil$.get(SparkHadoopUtil.scala:410)
     at org.apache.spark.deploy.yarn.ApplicationMaster$.main(ApplicationMaster.scala:796)
     at org.apache.spark.deploy.yarn.ExecutorLauncher$.main(ApplicationMaster.scala:821)
     at org.apache.spark.deploy.yarn.ExecutorLauncher.main(ApplicationMaster.scala)
    Caused by: java.lang.IllegalArgumentException: Can't get Kerberos realm
     at org.apache.hadoop.security.HadoopKerberosName.setConfiguration(HadoopKerberosName.java:65)
     at org.apache.hadoop.security.UserGroupInformation.initialize(UserGroupInformation.java:288)
     at org.apache.hadoop.security.UserGroupInformation.setConfiguration(UserGroupInformation.java:336)
     at org.apache.spark.deploy.SparkHadoopUtil.<init>(SparkHadoopUtil.scala:51)
     at org.apache.spark.deploy.yarn.YarnSparkHadoopUtil.<init>(YarnSparkHadoopUtil.scala:49)
     at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
     at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
     at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
     at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
     at java.lang.Class.newInstance(Class.java:442)
     at org.apache.spark.deploy.SparkHadoopUtil$.liftedTree1$1(SparkHadoopUtil.scala:387)
     ... 6 more
    Caused by: java.lang.reflect.InvocationTargetException
     at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
     at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
     at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
     at java.lang.reflect.Method.invoke(Method.java:498)
     at org.apache.hadoop.security.authentication.util.KerberosUtil.getDefaultRealm(KerberosUtil.java:88)
     at org.apache.hadoop.security.HadoopKerberosName.setConfiguration(HadoopKerberosName.java:63)
     ... 16 more
    Caused by: KrbException: Cannot locate default realm
     at sun.security.krb5.Config.getDefaultRealm(Config.java:1029)
     ... 22 more

Answer
------

In C80SPC200 and later, the file stored in the **/etc/krb5.conf** directory is no longer replaced during cluster installation. Instead, the file is stored in the corresponding path on the client through parameter configurations, and HiBench does not reference the client configuration file. Solution: Use the file stored in the **/opt/client/KrbClient/kerberos/var/krb5kdc/krb5.conf** directory on the client to overwrite that in the **/etc/krb5.conf** directories of all nodes. Make a backup before the overwriting.
