:original_name: mrs_01_24460.html

.. _mrs_01_24460:

How Do I Do If PostgreSQL or GaussDB Fails to Connect?
======================================================

-  Scenario 1: (**import** scenarios) Run the **sqoop import** command to extract the open source PostgreSQL to MRS HDFS or Hive.

   -  Symptom

      The **sqoop** command can be executed to query PostgreSQL tables, but an error is reported when the **sqoop import** command is executed.

      -  The authentication type 12 is not supported. Check that you have configured the pg_hba.conf file to include the client's IP address or subnet, and that it
      -  The authentication type 5 is not supported. Check that you have configured the pg_hba.conf file to include the client's IP address or subnet, and that it

   -  Root cause:

      -  If the authentication type is 5, the root cause is as follows: When the **sqoop import** command is executed, a MapReduce job is started. The PostgreSQL driver package **gsjdbc4-*.jar** exists in the MRS Hadoop installation directory **/opt/Bigdata/FusionInsight_HD_*/1_*_DataNode/install/hadoop/share/hadoop/common/lib**, which is incompatible with the open source PostgreSQL service. As a result, an error is reported.
      -  If the authentication type is 5, the root cause is as follows: The **pg_hba.conf** file of the database is incorrectly configured.

   -  Solution:

      -  If the authentication type is 5, the solution is as follows: Move the driver package **gsjdbc4-*.jar** to the **tmp** directory on each MRS core node.

         **mv /opt/Bigdata/FusionInsight_HD_*/1_*_DataNode/install/hadoop/share/hadoop/common/lib/gsjdbc4-*.jar /tmp**

      -  If the authentication type is 12, the solution is as follows: Modify the **pg_hba.conf** file of the database by changing the value of **ADDRESS** to the IP address of the node where Sqoop resides.

-  Scenario 2: (**export** scenarios) Run the **sqoop export** command to extract the open source PostgreSQL to MRS HDFS or Hive.

   -  Symptom

      The **sqoop** command can be executed to query PostgreSQL tables, but the error message "The authentication type 5 is not supported." is displayed when the **sqoop export** command is executed. Check that you have configured the pg_hba.conf file to include the client's IP address or subnet, and that it

   -  Root cause:

      When the **sqoop export** command is executed, a MapReduce job is started. The PostgreSQL driver package **gsjdbc4-*.jar** exists in the MRS Hadoop installation directory **/opt/Bigdata/FusionInsight_HD_*/1_*_DataNode/install/hadoop/share/hadoop/common/lib**, which is incompatible with the open-source PostgreSQL service. As a result, an error is reported.

   -  Solution:

      1. Move the driver package **gsjdbc4-*.jar** to the **tmp** directory on each MRS core node.

      **mv /opt/Bigdata/FusionInsight_HD_*/1_*_DataNode/install/hadoop/share/hadoop/common/lib/gsjdbc4-*.jar /tmp**

      2. Delete **/opt/Bigdata/client/Hive/Beeline/lib/gsjdbc4-*.jars**.
