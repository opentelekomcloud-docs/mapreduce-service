:original_name: ALM-45000.html

.. _ALM-45000:

ALM-45000 HetuEngine Service Unavailable
========================================

Description
-----------

The system checks the HetuEngine service status every 300 seconds. This alarm is generated when the HetuEngine service is unavailable.

This alarm is cleared when the HetuEngine service recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45000    Critical       Yes
======== ============== ==========

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

HetuEngine tasks fail to execute.

Possible Causes
---------------

-  The KrbServer service is abnormal.
-  The ZooKeeper service is abnormal.
-  The HDFS service is abnormal.
-  The Yarn service is abnormal.
-  The DBService service is abnormal.
-  The Hive service is abnormal.
-  Thre are no HSBroker instances in HetuEngine.

Procedure
---------

**Check the KrbServer service status.**

#. On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarm**.

#. In the alarm list, check whether the "ALM-25500 KrbServer Service Unavailable" alarm is generated.

   -  If yes, go to :ref:`3 <alm-45000__en-us_topic_0254455541_li6449155931114>`.
   -  If no, go to :ref:`5 <alm-45000__en-us_topic_0254455541_li9811171991313>`.

#. .. _alm-45000__en-us_topic_0254455541_li6449155931114:

   Clear "ALM-25500 KrbServer Service Unavailable" according to the alarm help.

#. In the alarm list, check whether the alarm "ALM-45000 HetuEngine Service Unavailable" is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45000__en-us_topic_0254455541_li9811171991313>`.

**Check the ZooKeeper service status.**

5. .. _alm-45000__en-us_topic_0254455541_li9811171991313:

   In the alarm list, check whether the alarm "ALM-12007 Process Fault" is generated.

   -  If yes, go to :ref:`6 <alm-45000__en-us_topic_0254455541_li078811388136>`.
   -  If no, go to :ref:`9 <alm-45000__en-us_topic_0254455541_li1453212224251>`.

6. .. _alm-45000__en-us_topic_0254455541_li078811388136:

   In the alarm list, click |image1| in the row that contains the "Process Fault" alarm. Check whether the name of the service for which the alarm is generated is ZooKeeper in **Location Information**.

   -  If yes, go to :ref:`7 <alm-45000__en-us_topic_0254455541_li8279173711910>`.
   -  If no, go to :ref:`9 <alm-45000__en-us_topic_0254455541_li1453212224251>`.

7. .. _alm-45000__en-us_topic_0254455541_li8279173711910:

   Clear "ALM-12007 Process Fault" according to the alarm help.

8. In the alarm list, check whether the alarm "ALM-45000 HetuEngine Service Unavailable" is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-45000__en-us_topic_0254455541_li1453212224251>`.

**Check the HDFS service status.**

9.  .. _alm-45000__en-us_topic_0254455541_li1453212224251:

    In the alarm list, check whether the "ALM-14000 HDFS Service Unavailable" alarm is generated.

    -  If yes, go to :ref:`10 <alm-45000__en-us_topic_0254455541_li11186103716269>`.
    -  If no, go to :ref:`12 <alm-45000__en-us_topic_0254455541_li164797109298>`.

10. .. _alm-45000__en-us_topic_0254455541_li11186103716269:

    Clear "ALM-14000 HDFS Service Unavailable" according to the alarm help.

11. In the alarm list, check whether the "ALM-45000 HetuEngine Service Unavailable" alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-45000__en-us_topic_0254455541_li164797109298>`.

**Check the YARN service status.**

12. .. _alm-45000__en-us_topic_0254455541_li164797109298:

    In the alarm list, check whether the "ALM-18000 YARN Service Unavailable" alarm is generated.

    -  If yes, go to :ref:`13 <alm-45000__en-us_topic_0254455541_li850063073216>`.
    -  If no, go to :ref:`15 <alm-45000__en-us_topic_0254455541_li1336315336331>`.

13. .. _alm-45000__en-us_topic_0254455541_li850063073216:

    Clear "ALM-18000 YARN Service Unavailable" according to the alarm help.

14. In the alarm list, check whether the "ALM-45000 HetuEngine Service Unavailable" alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`15 <alm-45000__en-us_topic_0254455541_li1336315336331>`.

**Check the DBService service status.**

15. .. _alm-45000__en-us_topic_0254455541_li1336315336331:

    In the alarm list, check whether the "ALM-27001 DBService Service Unavailable" alarm is generated.

    -  If yes, go to :ref:`16 <alm-45000__en-us_topic_0254455541_li1427826153416>`.
    -  If no, go to :ref:`20 <alm-45000__li9867630175315>`.

16. .. _alm-45000__en-us_topic_0254455541_li1427826153416:

    Clear "ALM-27001 DBService Service Unavailable" according to the alarm help.

17. In the alarm list, check whether the "ALM-45000 HetuEngine Service Unavailable" alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`20 <alm-45000__li9867630175315>`.

**Check the Hive service status.**

18. In the alarm list, check whether the "ALM-16004 Hive Service Unavailable" alarm is generated.

    -  If yes, go to :ref:`19 <alm-45000__en-us_topic_0254455541_li552411772716>`.
    -  If no, go to :ref:`20 <alm-45000__li9867630175315>`.

19. .. _alm-45000__en-us_topic_0254455541_li552411772716:

    Clear "ALM-16004 Hive Service Unavailable" according to the alarm help.

20. In the alarm list, check whether the "ALM-45000 HetuEngine Service Unavailable" alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`20 <alm-45000__li9867630175315>`.

**Check whether there are no HSBroker instances in HetuEngine.**

21. .. _alm-45000__li9867630175315:

    On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **HetuEngine**. On the page that is displayed, click the **Instance** tab.

22. Check whether there are no HSBroker instances.

    -  If yes, click **Add Instance** to add one.
    -  If no, go to :ref:`23 <alm-45000__en-us_topic_0254455541_li1994811814357>`.

23. In the alarm list, check whether the "ALM-45000 HetuEngine Service Unavailable" alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`23 <alm-45000__en-us_topic_0254455541_li1994811814357>`.

**Check the network connection between HetuEngine and ZooKeeper, HDFS, YARN, DBService, and Hive.**

24. .. _alm-45000__en-us_topic_0254455541_li1994811814357:

    On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **HetuEngine**. On the page that is displayed, click the **Instance** tab.

25. .. _alm-45000__en-us_topic_0254455541_li7948128193518:

    Click the host name in the **HSBroker** row and record the management IP address in the **Basic Information** area.

26. Log in to the host where HSBroker resides as user **omm** using the IP address obtained in :ref:`25 <alm-45000__en-us_topic_0254455541_li7948128193518>`.

27. Run the **ping** command to check whether the network connection between the host where HSBroker resides and the hosts where ZooKeeper, HDFS, Yarn, DBService, and Hive reside is in the normal state.

    -  If yes, go to :ref:`30 <alm-45000__en-us_topic_0254455541_li760014619484>`.
    -  If no, go to :ref:`28 <alm-45000__en-us_topic_0254455541_li10151810164812>`.

28. .. _alm-45000__en-us_topic_0254455541_li10151810164812:

    Contact the network administrator to restore the network.

29. In the alarm list, check whether the "ALM-45000 HetuEngine Service Unavailable" alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`30 <alm-45000__en-us_topic_0254455541_li760014619484>`.

**Collect fault information.**

30. .. _alm-45000__en-us_topic_0254455541_li760014619484:

    On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

31. Expand the **Service** drop-down list. In the **Services** dialog box that is displayed, select **HetuEngine** under the target cluster name, and click **OK**.

32. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the hosts to which the role belongs, and click **OK**.

33. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

34. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Reference
---------

None

.. |image1| image:: /_static/images/en-us_image_0000001532767734.png
.. |image2| image:: /_static/images/en-us_image_0000001532927662.png
