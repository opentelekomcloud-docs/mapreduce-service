:original_name: mrs_01_2112.html

.. _mrs_01_2112:

Why Cannot the Client Connect to ZooKeeper using the IBM JDK?
=============================================================

Question
--------

When the IBM JDK is used, the client fails to connect to ZooKeeper.

Answer
------

The possible cause is that the **jaas.conf** file format of the IBM JDK is different from that of the common JDK.

If IBM JDK is used, use the following **jaas.conf** template. The **useKeytab** file path must start with **file://**, followed by an absolute path.

.. code-block::

   Client {
   com.ibm.security.auth.module.Krb5LoginModule required
   useKeytab="file://D:/install/HbaseClientSample/conf/user.keytab"
   principal="hbaseuser1"
   credsType="both";
   };
