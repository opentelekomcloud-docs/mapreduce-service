:original_name: ALM-45001.html

.. _ALM-45001:

ALM-45001 Faulty HetuEngine Compute Instances
=============================================

This alarm applies only to MRS 3.2.0 or later.

Description
-----------

The system checks the HetuEngine compute instance status every 60 seconds. This alarm is generated when a HetuEngine compute instance is faulty.

This alarm is cleared when all faulty HetuEngine compute instances are restored.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45001    Major          Yes
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

-  The HDFS service is abnormal.
-  The Yarn service is abnormal.
-  Yarn queue resources are insufficient.
-  The process of compute instances is faulty.

Procedure
---------

**Check the HDFS service status.**

#. In the alarm list, check whether the "ALM-14000 HDFS Service Unavailable" alarm is generated.

   -  If yes, go to :ref:`2 <alm-45001__li775719097>`.
   -  If no, go to :ref:`4 <alm-45001__en-us_topic_0254455541_li164797109298>`.

#. .. _alm-45001__li775719097:

   Clear "ALM-14000 HDFS Service Unavailable" according to the alarm help.

#. In the alarm list, check whether the "ALM-45001 Faulty HetuEngine Compute Instances" alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-45001__en-us_topic_0254455541_li164797109298>`.

**Check the YARN service status.**

4. .. _alm-45001__en-us_topic_0254455541_li164797109298:

   In the alarm list, check whether the "ALM-18000 YARN Service Unavailable" alarm is generated.

   -  If yes, go to :ref:`5 <alm-45001__en-us_topic_0254455541_li850063073216>`.
   -  If no, go to :ref:`7 <alm-45001__li202811552178>`.

5. .. _alm-45001__en-us_topic_0254455541_li850063073216:

   Clear "ALM-18000 YARN Service Unavailable" according to the alarm help.

6. In the alarm list, check whether the "ALM-45001 Faulty HetuEngine Compute Instances" alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-45001__li202811552178>`.

**Check the YARN queue resource status.**

7. .. _alm-45001__li202811552178:

   In the alarm list, check whether the "ALM-18022 Insufficient YARN Queue Resources" alarm is generated.

   -  If yes, go to :ref:`8 <alm-45001__li151133170241>`.
   -  If no, go to :ref:`10 <alm-45001__en-us_topic_0254455541_li1994811814357>`.

8. .. _alm-45001__li151133170241:

   Clear "ALM-18022 Insufficient YARN Queue Resources" according to the alarm help.

9. In the alarm list, check whether the "ALM-45001 Faulty HetuEngine Compute Instances" alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-45001__en-us_topic_0254455541_li1994811814357>`.

**Check the HetuEngine compute instance status.**

10. .. _alm-45001__en-us_topic_0254455541_li1994811814357:

    Log in to FusionInsight Manager as an administrator who can access the HetuEngine web UI and choose **Cluster** > **Services** **> HetuEngine**.

11. In the **Basic Information** area on the **Dashboard** tab page, click the link next to **HSConsole WebUI** to access the HSConsole page.

12. On the compute instance page, check whether any compute instances are in the **FAULT** state.

    -  If yes, go to :ref:`13 <alm-45001__en-us_topic_0254455541_li854392104615>`.
    -  If no, go to :ref:`14 <alm-45001__en-us_topic_0254455541_li7665181304814>`.

13. .. _alm-45001__en-us_topic_0254455541_li854392104615:

    In the **Operation** column of the target compute instance, click **Start** and wait until the instance is started.

14. .. _alm-45001__en-us_topic_0254455541_li7665181304814:

    In the alarm list, check whether the "ALM-45001 Faulty HetuEngine Compute Instances" alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`15 <alm-45001__en-us_topic_0254455541_li760014619484>`.

**Collect fault information.**

15. .. _alm-45001__en-us_topic_0254455541_li760014619484:

    On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

16. Expand the **Service** drop-down list. In the **Services** dialog box that is displayed, select **HetuEngine** under the target cluster name, and click **OK**.

17. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the hosts to which the role belongs, and click **OK**.

18. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

19. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583127265.png
