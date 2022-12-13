:original_name: mrs_01_0418.html

.. _mrs_01_0418:

Sample Scripts
==============

Zeppelin
--------

Zeppelin is a web-based notebook that supports interactive data analysis. For more information, visit the Zeppelin official website at http://zeppelin.apache.org/.

This sample script is used to automatically install Zeppelin. Select the corresponding script path based on the region where the cluster is to be created. Enter the script path in **Script Path** on the **Bootstrap Action** page when adding a bootstrap action during cluster creation. You do not need to enter parameters for this script. Based on the Zeppelin usage habit, you only need to run the script on the active Master node.

-  Script path that you need to enter when adding the bootstrap action: s3a://mrs-samples-bootstrap-eu-de/zeppelin/zeppelin_install.sh
-  Path for downloading the sample script: https://mrs-samples-bootstrap-eu-de.obs.eu-de.otc.t-systems.com/zeppelin/zeppelin_install.sh

After the bootstrap action is complete, use either of the following methods to verify that Zeppelin is correctly installed.

Method 1: Log in to the active Master node as user **root** and run **/home/apache/zeppelin-0.7.3-bin-all/bin/zeppelin-daemon.sh status**. If the message stating "Zeppelin is running [ OK ]" is displayed, the installation is successful.

Method 2: Start a Windows ECS in the same VPC. Access port 7510 of the active Master node in the cluster. If the Zeppelin page is displayed, the installation is successful.

Presto
------

Presto is an open-source distributed SQL query engine, which is applicable to interactive analysis and query. For more information, visit the official website at http://prestodb.io/.

The sample script can be used to automatically install Presto. The script path is as follows:

-  Script path that you need to enter when adding the bootstrap action: s3a://mrs-samples-bootstrap-eu-de/presto/presto_install.sh
-  Path for downloading the sample script: https://mrs-samples-bootstrap-eu-de.obs.eu-de.otc.t-systems.com/presto/presto_install.sh

Based on the Presto usage habit, you are advised to install **dualroles** on the active Master nodes and **worker** on the Core nodes. You are advised to add the boot operation script and configure the parameters as follows:

.. table:: **Table 1** Bootstrap action script parameters

   +-----------------------------------+---------------------------------------------------------------------------------------+
   | Script 1                          | Name: install dualroles                                                               |
   |                                   |                                                                                       |
   |                                   | Script Path: Select the path of the **presto-install.sh** script based on the region. |
   |                                   |                                                                                       |
   |                                   | Execution Node: Active Master                                                         |
   |                                   |                                                                                       |
   |                                   | Parameters: dualroles                                                                 |
   |                                   |                                                                                       |
   |                                   | Execution Time: After component start                                                 |
   |                                   |                                                                                       |
   |                                   | Failed Action: Continue                                                               |
   +-----------------------------------+---------------------------------------------------------------------------------------+
   | Script 2                          | Name: install worker                                                                  |
   |                                   |                                                                                       |
   |                                   | Script Path: Select the path of the **presto-install.sh** script based on the region. |
   |                                   |                                                                                       |
   |                                   | Execution Node: Core                                                                  |
   |                                   |                                                                                       |
   |                                   | Parameters: worker                                                                    |
   |                                   |                                                                                       |
   |                                   | Execution Time: After component start                                                 |
   |                                   |                                                                                       |
   |                                   | Failed Action: Continue                                                               |
   +-----------------------------------+---------------------------------------------------------------------------------------+

After the bootstrap action is complete, you can start a Windows ECS in the same VPC of the cluster and access port 7520 of the active Master node to view the Presto web page.

You can also log in to the active Master node to try Presto and run the following commands as user **root**:

Command for loading the environment variable (In MRS 3.x and later versions, the default installation path of the client is /opt/Bigdata/client. In MRS 3.x and earlier versions, the default installation path is /opt/client. For details, see the actual situation.):

**#source /opt/Bigdata/client/bigdata_env**

Command for viewing the process status:

**#/home/apache/presto/presto-server-0.201/bin/launcher status**

Command for connecting to Presto and performing the operation

**#/home/apache/presto/presto-server-0.201/bin/presto --server localhost:7520 --catalog tpch --schema sf100**

**presto:sf100> select \* from nation;**

**presto:sf100> select count(*) from customer**
