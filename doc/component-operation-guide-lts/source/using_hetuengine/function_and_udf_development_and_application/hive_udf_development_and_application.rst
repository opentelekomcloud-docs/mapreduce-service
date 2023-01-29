:original_name: mrs_01_1743.html

.. _mrs_01_1743:

Hive UDF Development and Application
====================================

You can customize functions to extend SQL statements to meet personalized requirements. These functions are called UDFs.

This section describes how to develop and apply Hive UDFs.

Developing Hive UDFs
--------------------

This sample implements one Hive UDF described in the following table.

.. table:: **Table 1** Hive UDF

   ========== =====================================================
   Parameter  Description
   ========== =====================================================
   AutoAddOne Adds **1** to the input value and returns the result.
   ========== =====================================================

.. note::

   -  A common Hive UDF must be inherited from **org.apache.hadoop.hive.ql.exec.UDF**.

   -  A common Hive UDF must implement at least one **evaluate()**. The **evaluate** function supports overloading.

   -  Currently, only the following data types are supported:

      -  boolean, byte, short, int, long, float, and double
      -  Boolean, Byte, Short, Int, Long, Float, and Double
      -  List and Map

      UDFs, UDAFs, and UDTFs currently do not support complex data types other than the preceding ones.

   -  Currently, Hive UDFs supports only less than or equal to five input parameters. UDFs with more than five input parameters will fail to be registered.

   -  If the input parameter of a Hive UDF is **null**, the call returns **null** directly without parsing the Hive UDF logic. As a result, the UDF execution result may be inconsistent with the Hive execution result.

   -  To add the **hive-exec-3.1.1** dependency package to the Maven project, you can obtain the package from the Hive installation directory.

   -  (Optional) If the Hive UDF depends on a configuration file, you are advised to save the configuration file as a resource file in the **resources** directory so that it can be packed into the Hive UDF function package.

#. Create a Maven project. Set **groupId** to **com.test.udf** and **artifactId** to **udf-test**. The two values can be customized based on the site requirements.

#. Modify the **pom.xml** file as follows:

   .. code-block::

      <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
             <modelVersion>4.0.0</modelVersion>
             <groupId>com.test.udf</groupId>
             <artifactId>udf-test</artifactId>
             <version>0.0.1-SNAPSHOT</version>

             <dependencies>
               <dependency>
                  <groupId>org.apache.hive</groupId>
                  <artifactId>hive-exec</artifactId>
                  <version>3.1.1</version>
               </dependency>
             </dependencies>

             <build>
               <plugins>
                  <plugin>
                      <artifactId>maven-shade-plugin</artifactId>
                      <executions>
                          <execution>
                              <phase>package</phase>
                              <goals>
                                  <goal>shade</goal>
                              </goals>
                          </execution>
                      </executions>
                  </plugin>
                  <plugin>
                      <artifactId>maven-resources-plugin</artifactId>
                      <executions>
                          <execution>
                              <id>copy-resources</id>
                              <phase>package</phase>
                              <goals>
                                  <goal>copy-resources</goal>
                              </goals>
                              <configuration>
                                  <outputDirectory>${project.build.directory}/</outputDirectory>
                                  <resources>
                                      <resource>
                                          <directory>src/main/resources/</directory>
                                          <filtering>false</filtering>
                                      </resource>
                                  </resources>
                              </configuration>
                          </execution>
                      </executions>
                  </plugin>
               </plugins>
             </build>
      </project>

#. Create the implementation class of the Hive UDF.

   .. code-block::

      import org.apache.hadoop.hive.ql.exec.UDF;

      /**
       * AutoAddOne
       *
       * @since 2020-08-24
       */
      public class AutoAddOne extends UDF {
          public int evaluate(int data) {
              return data + 1;
          }
      }

#. Package the Maven project. The **udf-test-0.0.1-SNAPSHOT.jar** file in the **target** directory is the Hive UDF function package.

Configuring Hive UDFs
---------------------

In configuration file **udf.properties**, add registration information in the "Function_name Class_path" format to each line.

The following provides an example of registering four Hive UDFs in configuration file **udf.properties**:

.. code-block::

   booleanudf io.hetu.core.hive.dynamicfunctions.examples.udf.BooleanUDF
   shortudf io.hetu.core.hive.dynamicfunctions.examples.udf.ShortUDF
   byteudf io.hetu.core.hive.dynamicfunctions.examples.udf.ByteUDF
   intudf io.hetu.core.hive.dynamicfunctions.examples.udf.IntUDF

.. note::

   -  If the added Hive UDF registration information is incorrect, for example, the format is incorrect or the class path does not exist, the system ignores the incorrect registration information and prints the corresponding logs.
   -  If duplicate Hive UDFs are registered, the system will only register once and ignore the duplicate registrations.
   -  If the Hive UDF to be registered is the same as that already registered in the system, the system throws an exception and cannot be started properly. To solve this problem, you need to delete the Hive UDF registration information.

Deploying Hive UDFs
-------------------

To use an existing Hive UDF in HetuEngine, you need to upload the UDF function package, **udf.properties** file, and configuration file on which the UDF depends to the specified HDFS directory, for example, **/user/hetuserver/udf/**, and restart the HetuEngine compute instance.

#. Create the **/user/hetuserver/udf/data/externalFunctions** directory, save the **udf.properties** file in the **/user/hetuserver/udf** directory, save the UDF function package in the **/user/hetuserver/udf/data/externalFunctions** directory, and save the configuration files on which the UDF depends in the **/user/hetuserver/udf/data** directory.

   -  Upload the files on the HDFS page:

      a. Log in to FusionInsight Manager using the HetuEngine username and choose **Cluster** > **Services** > **HDFS**.
      b. In the **Basic Information** area on the **Dashboard** page, click the link next to **NameNode WebUI**.
      c. Choose **Utilities** > **Browse the file system** and click |image1| to create the **/user/hetuserver/udf/data/externalFunctions** directory.
      d. Go to **/user/hetuserver/udf** and click |image2| to upload the **udf.properties** file.
      e. Go to the **/user/hetuserver/udf/data/** directory and click |image3| to upload the configuration file on which the UDF depends.
      f. Go to the **/user/hetuserver/udf/data/externalFunctions** directory and click |image4| to upload the UDF function package.

   -  Use the HDFS CLI to upload the files.

      a. Log in to the node where the HDFS service client is located and switch to the client installation directory, for example, **/opt/client**.

         **cd /opt/client**

      b. Run the following command to configure environment variables:

         **source bigdata_env**

      c. If the cluster is in security mode, run the following command to authenticate the user. In normal mode, skip user authentication.

         **kinit** *HetuEngine* *username*

         Enter the password as prompted.

      d. Run the following commands to create directories and upload the prepared UDF function package, **udf.properties** file, and configuration file on which the UDF depends to the target directories:

         **hdfs dfs -mkdir** **/user/hetuserver/udf/data/externalFunctions**

         **hdfs dfs -put ./**\ *Configuration files on which the UDF depends* **/user/hetuserver/udf/data**

         **hdfs dfs -put ./udf.properties /user/hetuserver/udf**

         **hdfs dfs -put ./**\ *UDF function package* **/user/hetuserver/udf/data/externalFunctions**

#. Restart the HetuEngine compute instance.

Using Hive UDFs
---------------

Use a client to access a Hive UDF:

#. Log in to the HetuEngine client. For details, see :ref:`Using the HetuEngine Client <mrs_01_1737>`.

#. Run the following command to use a Hive UDF:

   **select AutoAddOne(1);**

   .. code-block::

      select AutoAddOne(1);
      _col0
      -------
           2
      (1 row)

.. |image1| image:: /_static/images/en-us_image_0000001295740228.png
.. |image2| image:: /_static/images/en-us_image_0000001349259325.png
.. |image3| image:: /_static/images/en-us_image_0000001349059877.png
.. |image4| image:: /_static/images/en-us_image_0000001296060032.png
