:original_name: mrs_01_24767.html

.. _mrs_01_24767:

Configuring Ranger Specifications
=================================

Scenario
--------

Ranger provides permission policies for services. When the number of service instances using Ranger increases, you need to adjust the specifications of Ranger.

.. note::

   This section applies only to MRS 3.2.0 or later.

Configuring Memory Parameters
-----------------------------

#. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Ranger**. Click **Configurations** then **All Configurations**, and search for **GC_OPTS** in the **RangerAdmin JVM** parameter. The default value of **GC_OPTS** is **-Dproc_rangeradmin -Xms2G -Xmx2G -XX:MaxDirectMemorySize=512M -XX:MetaspaceSize=100M -XX:MaxMetaspaceSize=200M -XX:PermSize=64M -XX:MaxPermSize=512M -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Xloggc:${RANGER_ADMIN_LOG_DIR}/gc-worker-%p-%t.log -XX:+UseGCLogFileRotation -XX:NumberOfGCLogFiles=20 -XX:GCLogFileSize=20M -verbose:gc -Djdk.tls.ephemeralDHKeySize=3072 -Djava.security.auth.login.config=#{conf_dir}/jaas.conf -Djava.security.krb5.conf=${KRB5_CONFIG} -Dbeetle.application.home.path=${BIGDATA_HOME}/common/runtime/security/config -Djna.tmpdir=${RANGER_TMP_HOME} -Djava.io.tmpdir=${RANGER_TMP_HOME} ${JAVA_STACK_PREFER} -Djdk.tls.rejectClientInitiatedRenegotiation=true**.

2. Change the value of **GC_OPTS** in the **RangerAdmin JVM** parameter as follows:

   Service instances that use Ranger include HDFS (NameNode), YARN (ResourceManager), HBase (HMaster and RegionServer), Hive (HiveServer), Kafka (Broker), Elasticsearch (EsNode, EsMaster, and EsClient), CDL (CDLService), and HetuEngine (HSBroker). When the number of these instances increases, change the default value **-Xms2G -Xmx2G** according to the reference RangerAdmin memory specifications listed below.

   ================ ===============
   Ranger Instances Reference Value
   ================ ===============
   200              -Xms4G -Xmx4G
   400              -Xms8G -Xmx8G
   600              -Xms12G -Xmx12G
   ================ ===============
