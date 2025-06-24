:original_name: mrs_03_1244.html

.. _mrs_03_1244:

How Do I Interconnect MRS with LTS?
===================================

Prerequisites
-------------

You have obtained the account AK and SK. For details, see `How Do I Manage Access Keys? <https://docs.otc.t-systems.com/identity-access-management/mycredential/how_do_i_manage_access_keys.html>`__

Procedure
---------

#. .. _mrs_03_1244__li95619136447:

   Install ICAgent on the MRS node. For details, see `Installing ICAgent <https://docs.otc.t-systems.com/log-tank-service/umn/getting_started/installing_icagent.html>`__.

   .. note::

      For the first installation, install one server first, and then batch install all other hosts in the same way.

#. .. _mrs_03_1244__li11114745132412:

   Create a host group and add the ICAgent host installed in :ref:`1 <mrs_03_1244__li95619136447>` to the host group.

   a. Log in to the Log Tank Service (LTS) console, and choose **Host Management** in the left navigation pane. On the displayed page, click **Create Host Group** in the upper right corner.
   b. In the **Create Host Group** slide-out panel that is displayed, enter a host group name in the **Host Group** field and set **Host OS** to **Linux** or **Windows**.
   c. In the host list, select one or more hosts to add to the group and click **OK**.

      -  You can filter hosts by host name or host IP address. You can also click **Search by Host IP Address** and enter multiple host IP addresses in the displayed search box to search for matches.
      -  If your desired hosts are not in the list, click **Install ICAgent**. In the **Install ICAgent** slide-out panel displayed, install ICAgent on the hosts as prompted.

#. Create a log group.

   a. Log in to the LTS console. On the **Log Management** page, click **Create Log Group**.

   b. In the **Create Log Group** slide-out panel displayed, enter a log group name. A log group name:

      -  Can contain only letters, numbers, hyphens (-), underscores (_), and periods (.).
      -  Cannot start with a period (.) or underscore (_), and cannot end with a period (.).
      -  Can contain 1 to 64 characters.

   c. Select an enterprise project. You can click **View Enterprise Projects** to view all enterprise projects.

   d. Set **Log Retention Duration**. The system stores logs for 30 days by default. You can change the log retention duration after the log group is created.

      LTS offers a free quota of 500 MB per month for log read/write, retention, and indexing. When the free quota is used up, you will be billed for excess usage on a pay-per-use basis.

   e. Click **OK**.

      -  On the **Log Management** page, you can view log group details, including name, retention duration, creation time, creation type, and tags. You can also modify retention duration and tags. Click **Modify** in the **Operation** column of the log group to modify the name and retention duration.
      -  Click the log group name to access the log stream details page.

#. Create a log stream.

   a. On the LTS console, click the expansion button of a log group.

   b. Click **Create Log Stream**. In the **Create Log Stream** slide-out panel displayed, enter a log stream name. A log stream name:

      -  Can contain only letters, numbers, hyphens (-), underscores (_), and periods (.).
      -  Cannot start with a period (.) or underscore (_), and cannot end with a period (.).
      -  Can contain 1 to 64 characters.

   c. Select an enterprise project. You can click **View Enterprise Projects** to view all enterprise projects.

   d. Click **OK**.

      On the log stream page, you can view details of the log stream, including log stream name, enterprise project, log retention duration, creation time, and creation type.

      .. note::

         You can configure different log streams for different components.

#. Add hosts for log ingestion.

   a. In the navigation pane of the LTS management console, choose **Log Ingestion** > **Ingestion Center**.

   b. On the **All** tab page displayed, click **Elastic Cloud Server (ECS)**.

   c. In the **Select Log Stream** step, set **Log Group** and **Log Stream** to the created log group and log stream name, and click **Next**.

   d. In the **(Optional) Select Host Group** step, select the host group created in :ref:`2 <mrs_03_1244__li11114745132412>` and click **Next**.

   e. In the **Collections** step, set **Collection Configuration Name** and **Collection Paths**, and click **Next**.

      .. note::

         Path configurations

         -  You can configure multiple collection paths by clicking **Add Collection Path**.
         -  Each collection path must be unique. That is, the same path of the same host cannot be configured for different log groups and log streams.
         -  Collection paths support recursion. You can use double asterisks (**) to collect logs from up to five directory levels.
         -  Collection paths support fuzzy match. You can use an asterisk (*) to represent one or more characters of a directory or file name.
         -  If the collection path is set to a directory (such as **/var/logs/**), only **.log**, **.trace**, and **.out** files in the directory are collected.

      For example, configure the following collection paths:

      YARN task log path:

      ::

         /srv/BigData/*/nm/containerlogs/**/container-localizer-syslog
         /srv/BigData/*/nm/containerlogs/**/directory.info
         /srv/BigData/*/nm/containerlogs/**/launch_container.sh
         /srv/BigData/*/nm/containerlogs/**/prelaunch.err
         /srv/BigData/*/nm/containerlogs/**/prelaunch.out
         /srv/BigData/*/nm/containerlogs/**/stderr
         /srv/BigData/*/nm/containerlogs/**/stdout
         /srv/BigData/*/nm/containerlogs/**/syslog*
         /srv/BigData/*/nm/containerlogs/**/*.log

      All HDFS service logs:

      ::

         /var/log/Bigdata/audit/hdfs/jn/hdfs-audit-journalnode.log
         /var/log/Bigdata/audit/hdfs/jn/SecurityAuth.audit
         /var/log/Bigdata/hdfs/*/

      Configure log collection paths for other components by referring to HDFS service logs.

   f. Skip the **Index Settings** step and submit.

      .. note::

         For details about how to configure index settings, see the *Log Tank Service User Guide*.

#. View the logs.

   a. Log in to the LTS console and choose **Log Management** in the navigation pane.
   b. In the **Log Group Name** column, click the name of the created log group to view logs.
