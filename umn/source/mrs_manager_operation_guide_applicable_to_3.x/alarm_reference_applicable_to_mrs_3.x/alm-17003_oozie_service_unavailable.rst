:original_name: ALM-17003.html

.. _ALM-17003:

ALM-17003 Oozie Service Unavailable
===================================

Description
-----------

The system checks the Oozie service status in every 5 seconds. This alarm is generated when Oozie or a component on which Oozie depends cannot provide services properly.

This alarm is automatically cleared when the Oozie service recovers.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
17003    Critical       Yes
======== ============== =====================

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

Oozie cannot be used to submit jobs.

Possible Causes
---------------

-  The DBService service is abnormal or the data of Oozie stored in DBService is damaged.
-  The HDFS service is abnormal or the data of Oozie stored in HDFS is damaged.
-  The Yarn service is abnormal.
-  The Nodeagent process is abnormal.

Procedure
---------

**Query the Oozie service health status code.**

#. On the MRS Manager portal, choose **Cluster** > *Name of the desired cluster* >\ **Services** > **Oozie**. Click **oozie** (any one is OK) on the **oozie WebUI**. to go to the Oozie WebUI.

   .. note::

      By default, the **admin** user does not have the permissions to manage other components. If the page cannot be opened or the displayed content is incomplete when you access the native UI of a component due to insufficient permissions, you can manually create a user with the permissions to manage that component.

#. Add **/servicehealth** to the URL in the address box of the browser and access again. The value of **statusCode** is the current Oozie service health status code.

   For example, visit **https://10.10.0.117:20026/Oozie/oozie/130/oozie/servicehealth**. The result is as follows:

   .. code-block::

      {"beans":[{"name":"serviceStatus","statusCode":0}]}

   If the health status code cannot be displayed or the browser does not respond, the service may be unavailable due to Oozie process fault. See :ref:`13 <alm-17003__li3460735817821>` to rectify the fault.

#. Perform the operations based on the error code. For details, see :ref:`Table 1 <alm-17003__table1418843217821>`.

   .. _alm-17003__table1418843217821:

   .. table:: **Table 1** Oozie service health status code

      +-------------+------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------+
      | Status Code | Description                        | Error Cause                                                                     | Solution                                    |
      +=============+====================================+=================================================================================+=============================================+
      | 0           | The service is running properly.   | None                                                                            | None                                        |
      +-------------+------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------+
      | 18002       | The DBService service is abnormal. | Oozie fails to connect to DBService or the data stored in DBService is damaged. | See :ref:`4 <alm-17003__li5899993317821>`.  |
      +-------------+------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------+
      | 18003       | The HDFS service is abnormal.      | Oozie fails to connect to HDFS or the data stored in HDFS is damaged.           | See :ref:`7 <alm-17003__li6587172717821>`.  |
      +-------------+------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------+
      | 18005       | The MapReduce service is abnormal. | The Yarn service is abnormal.                                                   | See :ref:`11 <alm-17003__li6500500117821>`. |
      +-------------+------------------------------------+---------------------------------------------------------------------------------+---------------------------------------------+

**Check the DBService service.**

4. .. _alm-17003__li5899993317821:

   On the MRS Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services**, and check whether the DBService service is running properly.

   -  If yes, go to :ref:`6 <alm-17003__li2491190317821>`.
   -  If no, go to :ref:`5 <alm-17003__li6459530417821>`.

5. .. _alm-17003__li6459530417821:

   Resolve the problem of DBService based on the alarm help and check whether the Oozie alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`18 <alm-17003__li3980393617821>`.

6. .. _alm-17003__li2491190317821:

   Log in to the Oozie database to check whether the data is complete.

   a. Log in to the active DBService node as user **root**.

      On the MRS Manager page, choose **Cluster** > *Name of the desired cluster* > **Services** > **DBService > Instance** to view the IP address of the active DBservice node.

   b. Run the following command to log in to the Oozie database:

      **su - omm**

      **source ${BIGDATA_HOME}/FusionInsight_BASE\_8.1.0.1/install/FusionInsight-dbservice-2.7.0/.dbservice_profile**

      **gsql -U** *Username* **-W** *Oozie database password* **-p 20051 -d** *Database name*

   c. After the login is successful, enter **\\d** to check whether there are 15 data tables.

      The Oozie service has 15 data tables by default. If these data tables are deleted or the table structure is modified, the Oozie service may be unavailable. Contact the O&M personnel to back up the data and perform restoration.

**Check the HDFS service.**

7.  .. _alm-17003__li6587172717821:

    On the MRS Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services**, and check whether the HDFS service is running properly.

    -  If yes, go to :ref:`9 <alm-17003__li940532017821>`.
    -  If no, go to :ref:`8 <alm-17003__li2988812617821>`.

8.  .. _alm-17003__li2988812617821:

    Resolve the problem of HDFS based on the alarm help and check whether the Oozie alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`18 <alm-17003__li3980393617821>`.

9.  .. _alm-17003__li940532017821:

    Log in to HDFS to check whether the Oozie file directory structure is complete.

    a. Download and install an HDFS client..

    b. Log in to the client node as user **root** and run the following commands to check whether **/user/oozie/share** exists.

       If the cluster uses the security mode, perform security authentication.

       **kinit admin**

       **hdfs dfs -ls /user/oozie/share**

    -  If yes, go to :ref:`18 <alm-17003__li3980393617821>`.
    -  If no, go to :ref:`10 <alm-17003__li367846717821>`.

10. .. _alm-17003__li367846717821:

    In the Oozie client installation directory, manually upload the share directory to **/user/oozie** in HDFS, and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`18 <alm-17003__li3980393617821>`.

**Check the Yarn and MapReduce service.**

11. .. _alm-17003__li6500500117821:

    On the MRS Manager portal, choose **Cluster >** *Name of the desired cluster* > **Services**, and check whether the Yarn and MapReduce services are running properly.

    -  If yes, go to :ref:`18 <alm-17003__li3980393617821>`.
    -  If no, go to :ref:`12 <alm-17003__li2196836817821>`.

12. .. _alm-17003__li2196836817821:

    Resolve the problem of Yarn and MapReduce based on the alarm help and check whether the Oozie alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`18 <alm-17003__li3980393617821>`.

**Check the Oozie process.**

13. .. _alm-17003__li3460735817821:

    Log in to each node of Oozie as user **root**.

14. Run the **ps -ef \| grep oozie** command to check whether the Oozie process exists.

    -  If yes, go to :ref:`15 <alm-17003__li1524116517821>`.
    -  If no, go to :ref:`18 <alm-17003__li3980393617821>`.

15. .. _alm-17003__li1524116517821:

    Collect fault information in **prestartDetail.log**, **oozie.log**, and **catalina.out** in the Oozie log directory **/var/log/Bigdata/oozie**. If the alarm is not caused by manual misoperation, go to :ref:`16 <alm-17003__li3722887217821>`.

**Check the Nodeagent process.**

16. .. _alm-17003__li3722887217821:

    Log in to each node of Oozie as user **root**. Run the **ps -ef \| grep nodeagent** command to check whether the Nodeagent process exists.

    -  If yes, go to :ref:`17 <alm-17003__li2866055917821>`.
    -  If no, go to :ref:`18 <alm-17003__li3980393617821>`.

17. .. _alm-17003__li2866055917821:

    Run the **kill -9** *The process ID of nodeagent* command, wait 10 minutes, and check whether alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`18 <alm-17003__li3980393617821>`.

18. .. _alm-17003__li3980393617821:

    Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None
