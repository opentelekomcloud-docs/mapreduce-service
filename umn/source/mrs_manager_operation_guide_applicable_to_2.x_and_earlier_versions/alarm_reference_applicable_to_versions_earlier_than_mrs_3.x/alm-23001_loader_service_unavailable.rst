:original_name: alm_23001.html

.. _alm_23001:

ALM-23001 Loader Service Unavailable
====================================

Description
-----------

The system checks the Loader service availability every 60 seconds. This alarm is generated if the Loader service is unavailable and is cleared after the Loader service recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
23001    Critical       Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Parameter   Description
=========== =======================================================
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

Data loading, import, and conversion are unavailable.

Possible Causes
---------------

-  The services that Loader depends on are abnormal.

   -  ZooKeeper is abnormal.
   -  HDFS is abnormal.
   -  DBService is abnormal.
   -  Yarn is abnormal.
   -  MapReduce is abnormal.

-  The network is faulty. Loader cannot communicate with its dependent services.
-  Loader is running improperly.

Procedure
---------

#. Check the ZooKeeper status.

   a. Go to the MRS cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. Choose **ZooKeeper** and check whether the health status of ZooKeeper is normal.

      -  If yes, go to :ref:`1.d <alm_23001__en-us_topic_0191813961_li173182016530>`.
      -  If no, go to :ref:`1.c <alm_23001__en-us_topic_0191813961_li4731152065314>`.

   c. .. _alm_23001__en-us_topic_0191813961_li4731152065314:

      Choose **More > Restart Service** to restart ZooKeeper. After ZooKeeper starts, check whether the "ALM-23001 Loader Service Unavailable" alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`1.d <alm_23001__en-us_topic_0191813961_li173182016530>`.

   d. .. _alm_23001__en-us_topic_0191813961_li173182016530:

      On MRS Manager, check whether the ALM-12007 Process Fault alarm is reported.

      -  If yes, go to :ref:`1.e <alm_23001__en-us_topic_0191813961_li11731152014534>`.
      -  If no, go to :ref:`2.a <alm_23001__en-us_topic_0191813961_li103551920123512>`.

   e. .. _alm_23001__en-us_topic_0191813961_li11731152014534:

      In **Alarm Details** of the "ALM-12007 Process Fault" alarm, check whether **ServiceName** is **ZooKeeper**.

      -  If yes, go to :ref:`1.f <alm_23001__en-us_topic_0191813961_li167320209539>`.
      -  If no, go to :ref:`2.a <alm_23001__en-us_topic_0191813961_li103551920123512>`.

   f. .. _alm_23001__en-us_topic_0191813961_li167320209539:

      Clear the alarm according to the handling suggestions of "ALM-12007 Process Fault".

   g. Check whether the "ALM-23001 Loader Service Unavailable" alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.a <alm_23001__en-us_topic_0191813961_li103551920123512>`.

#. Check the HDFS status.

   a. .. _alm_23001__en-us_topic_0191813961_li103551920123512:

      Go to the MRS cluster details page and choose **Alarms**.

   b. On MRS Manager, check whether the "ALM-14000 HDFS Service Unavailable alarm" is reported.

      -  If yes, go to :ref:`2.c <alm_23001__en-us_topic_0191813961_li167011853195320>`.
      -  If no, go to :ref:`3.a <alm_23001__en-us_topic_0191813961_li1554455818353>`.

   c. .. _alm_23001__en-us_topic_0191813961_li167011853195320:

      Clear the alarm according to the handling suggestions of "ALM-14000 HDFS Service Unavailable".

   d. Check whether the "ALM-23001 Loader Service Unavailable" alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3.a <alm_23001__en-us_topic_0191813961_li1554455818353>`.

#. Check the DBService status.

   a. .. _alm_23001__en-us_topic_0191813961_li1554455818353:

      Go to the MRS cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. Choose **DBService** to check whether the health status of DBService is normal.

      -  If yes, go to :ref:`4.a <alm_23001__en-us_topic_0191813961_li14598145163614>`.
      -  If no, go to :ref:`3.c <alm_23001__en-us_topic_0191813961_li122981864542>`.

   c. .. _alm_23001__en-us_topic_0191813961_li122981864542:

      Choose **More > Restart Service** to restart DBService. After DBService starts, check whether the "ALM-23001 Loader Service Unavailable" alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4.a <alm_23001__en-us_topic_0191813961_li14598145163614>`.

#. Check the MapReduce status.

   a. .. _alm_23001__en-us_topic_0191813961_li14598145163614:

      Go to the MRS cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. Choose **MapReduce** and check whether the health status of MapReduce is normal.

      -  If yes, go to :ref:`5.a <alm_23001__en-us_topic_0191813961_li984194223716>`.
      -  If no, go to :ref:`4.c <alm_23001__en-us_topic_0191813961_li191227237549>`.

   c. .. _alm_23001__en-us_topic_0191813961_li191227237549:

      Choose **More > Restart Service** to restart MapReduce. After MapReduce starts, check whether the "ALM-23001 Loader Service Unavailable" alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`5.a <alm_23001__en-us_topic_0191813961_li984194223716>`.

#. Check the Yarn status.

   a. .. _alm_23001__en-us_topic_0191813961_li984194223716:

      Go to the MRS cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. Choose **Yarn** and check whether the health status of Yarn is normal.

      -  If yes, go to :ref:`5.d <alm_23001__en-us_topic_0191813961_li11673173775413>`.
      -  If no, go to :ref:`5.c <alm_23001__en-us_topic_0191813961_li126731375547>`.

   c. .. _alm_23001__en-us_topic_0191813961_li126731375547:

      Choose **More > Restart Service** to restart Yarn. After Yarn starts, check whether the "ALM-23001 Loader Service Unavailable" alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`5.d <alm_23001__en-us_topic_0191813961_li11673173775413>`.

   d. .. _alm_23001__en-us_topic_0191813961_li11673173775413:

      On MRS Manager, check whether the "ALM-18000 Yarn Service Unavailable" alarm is reported.

      -  If yes, go to :ref:`5.e <alm_23001__en-us_topic_0191813961_li6673837155415>`.
      -  If no, go to :ref:`6.a <alm_23001__en-us_topic_0191813961_li13825217113813>`.

   e. .. _alm_23001__en-us_topic_0191813961_li6673837155415:

      Clear the alarm according to the handling suggestions of "ALM-18000 Yarn Service Unavailable".

   f. Check whether the "ALM-23001 Loader Service Unavailable" alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`6.a <alm_23001__en-us_topic_0191813961_li13825217113813>`.

#. Check the network connections between Loader and its dependent components.

   a. .. _alm_23001__en-us_topic_0191813961_li13825217113813:

      Go to the MRS cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. Click **Loader**.

   c. Click **Instance**. The Sqoop instance list is displayed.

   d. .. _alm_23001__en-us_topic_0191813961_li2928194985415:

      Record the management IP addresses of all Sqoop instances.

   e. Log in to the hosts using the IP addresses obtained in :ref:`6.d <alm_23001__en-us_topic_0191813961_li2928194985415>`. Run the following commands to switch the user:

      **sudo su - root**

      **su - omm**

   f. Run the **ping** command to check whether the network connection between the hosts where the Sqoop instances reside and the dependent components is normal. (The dependent components include ZooKeeper, DBService, HDFS, MapReduce, and Yarn. The method to obtain the IP addresses of the dependent components is the same as that used to obtain the IP addresses of the Sqoop instances.)

      -  If yes, go to :ref:`7 <alm_23001__en-us_topic_0191813961_li572522141314>`.
      -  If no, go to :ref:`6.g <alm_23001__en-us_topic_0191813961_li10928124925412>`.

   g. .. _alm_23001__en-us_topic_0191813961_li10928124925412:

      Contact the network administrator to repair the network.

   h. Check whether the "ALM-23001 Loader Service Unavailable" alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`7 <alm_23001__en-us_topic_0191813961_li572522141314>`.

#. .. _alm_23001__en-us_topic_0191813961_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.
