:original_name: mrs_01_1976.html

.. _mrs_01_1976:

Data Serialization
==================

Scenario
--------

Spark supports the following types of serialization:

-  JavaSerializer
-  KryoSerializer

Data serialization affects the Spark application performance. In specific data format, KryoSerializer offers 10X higher performance than JavaSerializer. For Int data, performance optimization can be ignored.

KryoSerializer depends on Chill of Twitter. Not all Java Serializable objects support KryoSerializer. Therefore, class must be manually registered.

Serialization involves task serialization and data serialization. Only JavaSerializer can be used for Spark task serialization. JavaSerializer and KryoSerializer can be used for data serialization.

Procedure
---------

When the Spark program is running, a large volume of data needs to be serialized during the shuffle and RDD cache procedures. By default, JavaSerializer is used. You can also configure KryoSerializer as the data serializer to improve serialization performance.

Add the following code to enable KryoSerializer to be used:

-  Implement the class registrar and manually register the class.

   .. code-block::

      package com.etl.common;

      import com.esotericsoftware.kryo.Kryo;
      import org.apache.spark.serializer.KryoRegistrator;

      public class DemoRegistrator implements KryoRegistrator
      {
          @Override
          public void registerClasses(Kryo kryo)
          {
              //Class examples are given below. Register the custom classes.
              kryo.register(AggrateKey.class);
              kryo.register(AggrateValue.class);
          }
      }

   You can configure **spark.kryo.registrationRequired** on Spark client. Whether to require registration with Kryo. If set to 'true', Kryo will throw an exception if an unregistered class is serialized. If set to false (the default), Kryo will write unregistered class names along with each object. Writing class names can cause significant performance overhead. This operation will affect the system performance. If the value of **spark.kryo.registrationRequired** is configured to **true**, you need to manually register the class. For a class that is not serialized, the system will not automatically write the class name, but display an exception. Compare the configuration of **true** with that of **false**, the configuration of **true** has the better performance.

-  Configure KryoSerializer as the data serializer and class registrar.

   .. code-block::

      val conf = new SparkConf()
      conf.set("spark.serializer", "org.apache.spark.serializer.KryoSerializer")
      .set("spark.kryo.registrator", "com.etl.common.DemoRegistrator")
