:original_name: mrs_01_2339.html

.. _mrs_01_2339:

HetuEngine Function Plugin Development and Application
======================================================

You can customize functions to extend SQL statements to meet personalized requirements. These functions are called UDFs.

This section describes how to develop and apply HetuEngine function plugins.

Developing Function Plugins
---------------------------

This sample implements two function plugins described in the following table.

.. table:: **Table 1** HetuEngine function plugins

   +------------+----------------------------------------------------------------------------------------------------------------+---------------------+
   | Parameter  | Description                                                                                                    | Type                |
   +============+================================================================================================================+=====================+
   | add_two    | Adds **2** to the input integer and returns the result.                                                        | ScalarFunction      |
   +------------+----------------------------------------------------------------------------------------------------------------+---------------------+
   | avg_double | Aggregates and calculates the average value of a specified column. The field type of the column is **double**. | AggregationFunction |
   +------------+----------------------------------------------------------------------------------------------------------------+---------------------+

#. Create a Maven project. Set **groupId** to **com.test.udf** and **artifactId** to **udf-test**. The two values can be customized based on the site requirements.

#. Modify the **pom.xml** file as follows:

   .. code-block::

      <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
             <modelVersion>4.0.0</modelVersion>
             <groupId>com.test.udf</groupId>
             <artifactId>udf-test</artifactId>
             <version>0.0.1-SNAPSHOT</version>

             <packaging>hetu-plugin</packaging>

             <dependencies>
                 <dependency>
                     <groupId>com.google.guava</groupId>
                     <artifactId>guava</artifactId>
                     <version>26.0-jre</version>
                 </dependency>

                 <dependency>
                     <groupId>io.hetu.core</groupId>
                     <artifactId>presto-spi</artifactId>
                     <version>1.2.0</version>
                     <scope>provided</scope>
                 </dependency>

             </dependencies>

             <build>
                 <plugins>
                     <plugin>
                         <groupId>org.apache.maven.plugins</groupId>
                         <artifactId>maven-assembly-plugin</artifactId>
                         <version>2.4.1</version>
                         <configuration>
                             <encoding>UTF-8</encoding>
                         </configuration>
                     </plugin>
                     <plugin>
                         <groupId>io.hetu</groupId>
                         <artifactId>presto-maven-plugin</artifactId>
                         <version>9</version>
                         <extensions>true</extensions>
                     </plugin>
                 </plugins>
             </build>
         </project>

#. Create the implementation class of the function plugin.

   1. Create the function plugin implementation class **com.hadoop.other.TestUDF4**. The code is as follows:

   .. code-block::

      public class TestUDF4 {
           @ScalarFunction("add_two")
           @SqlType(StandardTypes.INTEGER)
           public static long add2(@SqlNullable @SqlType(StandardTypes.INTEGER) Long i)      {
               return i+2;
      }

   2. Create the function plugin implementation class **com.hadoop.other.AverageAggregation**. The code is as follows:

   .. code-block::

      @AggregationFunction("avg_double")
      public class AverageAggregation
      {
          @InputFunction
          public static void input(
              LongAndDoubleState state,
              @SqlType(StandardTypes.DOUBLE) double value)
          {
              state.setLong(state.getLong() + 1);
              state.setDouble(state.getDouble() + value);
          }

          @CombineFunction
          public static void combine(
              LongAndDoubleState state,
              LongAndDoubleState otherState)
          {
              state.setLong(state.getLong() + otherState.getLong());
              state.setDouble(state.getDouble() + otherState.getDouble());
          }

          @OutputFunction(StandardTypes.DOUBLE)
          public static void output(LongAndDoubleState state, BlockBuilder out)
          {
              long count = state.getLong();
              if (count == 0) {
                  out.appendNull();
              }
              else {
                  double value = state.getDouble();
                  DOUBLE.writeDouble(out, value / count);
              }
          }
      }

#. Create the **com.hadoop.other.LongAndDoubleState** API on which **AverageAggregation** depends.

   .. code-block::

      public interface LongAndDoubleState extends AccumulatorState {
         long getLong();

         void setLong(long value);

         double getDouble();

         void setDouble(double value);
      }

#. Create the function plugin registration class **com.hadoop.other.RegisterFunctionTestPlugin**. The code is as follows:

   .. code-block::

      public class RegisterFunctionTestPlugin implements Plugin {

          @Override
          public Set<Class<?>> getFunctions() {
              return ImmutableSet.<Class<?>>builder()
                      .add(TestUDF4.class)
                      .add(AverageAggregation.class)
                      .build();
          }
      }

#. Pack the Maven project and obtain the **udf-test-0.0.1-SNAPSHOT** directory in the **target** directory. The following figure shows the overall structure of the project.

   |image1|

Deploying Function Plugins
--------------------------

Before the deployment, ensure that:

-  The HetuEngine service is normal.
-  The HDFS and HetuEngine client have been installed on the cluster node, for example, in the **/opt/client** directory.
-  A HetuEngine user has been created. For details about how to create a user, see :ref:`Creating a HetuEngine User <mrs_01_1714>`.

#. Upload the **udf-test-0.0.1-SNAPSHOT** directory obtained in packing the Maven project to any directory on the node where the client is installed.
#. Upload the **udf-test-0.0.1-SNAPSHOT** directory to HDFS.

   a. Log in to the node where the client is installed and perform security authentication.

      **cd /opt/client**

      **source bigdata_env**

      **kinit** *HetuEngine user*

      Enter the password as prompted and change the password upon the first authentication.

   b. Create the following paths in HDFS. If the paths already exist, skip this step.

      **hdfs dfs -mkdir -p /user/hetuserver/udf/data/externalFunctionsPlugin**

   c. Upload the **udf-test-0.0.1-SNAPSHOT** directory to HDFS.

      **hdfs dfs -put udf-test-0.0.1-SNAPSHOT /user/hetuserver/udf/data/externalFunctionsPlugin**

   d. Change the directory owner and owner group.

      **hdfs dfs -chown -R hetuserver:hadoop /user/hetuserver/udf/data**

#. Restart the HetuEngine compute instance.

Verifying Function Plugins
--------------------------

#. Log in to the node where the client is installed and perform security authentication.

   **cd /opt/client**

   **source bigdata_env**

   **kinit** *HetuEngine user*

   **hetu-cli --catalog hive --schema default**

#. Verify function plugins.

   a. Query a table.

      **select \* from test1;**

      .. code-block::

         select * from test1;
         name  |  price
         --------|-------
         apple   |  17.8
         orange |  25.0
         (2 rows)

   b. Return the average value.

      **select avg_double(price) from test1;**

      .. code-block::

         select avg_double(price) from test1;
         _col0
         -------
           21.4
         (1 row)

   c. Return the value of the input integer plus 2.

      **select add_two(4);**

      .. code-block::

         select add_two(4);
         _col0
         -------
             6
         (1 row)

.. |image1| image:: /_static/images/en-us_image_0000001295740088.png
