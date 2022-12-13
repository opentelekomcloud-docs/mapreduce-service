:original_name: admin_guide_000033.html

.. _admin_guide_000033:

Collecting Stack Information
============================

Scenario
--------

To meet actual service requirements, the cluster administrator can collect stack information about a specified role or instance on FusionInsight Manager, save the information to a local directory, and download the information. The following information can be collected:

#. jstack information.
#. jmap -histo information.
#. jmap -dump information.
#. Thr jstack and jmap-histo information can be collected continuously for comparison.

Procedure
---------

**Collecting stack information**

#. Log in to FusionInsight Manager.
#. Click **Cluster**, click the name of the desired cluster, click **Services**, and click the target service.
#. On the displayed page, Choose **More** > **Collect Stack Information**.

   .. note::

      -  To collect stack information of multiple instances, go to the instance list, select the desired instances in the instance list and choose **More** > **Collect Stack Information**.
      -  To collect stack information of a single instance, click the desired instance and choose **More** > **Collect Stack Information**.

#. In the displayed dialog box, select the desired role and content, configure advanced options (retain the default settings if there is no special requirement), and click **OK**.
#. After the collection is successful, click **Download**.

**Downloading Stack Information**

6. Click **Cluster**, click the name of the desired cluster, click **Services**, and click the target service. Choose **More** > **Download Stack Information** in the upper right corner.
7. Select the desired role and content and click **Download** to download the stack information to the local PC.

**Clearing stack information**

8.  Click **Cluster**, click the name of the desired cluster, click **Services**, and click the target service.
9.  Choose **More** > **Clear Stack Information** in the upper right corner.
10. Select the desired role and content and configure **File Directory**. Click **OK**.
