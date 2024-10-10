:original_name: mrs_01_248991.html

.. _mrs_01_248991:

Interconnecting Flink with OBS
==============================

Interconnecting with OBS
------------------------

#. Log in to the Flink client installation node as the client installation user.

#. Run the following command to initialize environment variables:

   **source** *Client installation directory*\ **/bigdata_env**

#. Configure the Flink client.

#. Start a session.

   -  Normal cluster (Kerberos authentication disabled)

      **yarn-session.sh -nm "**\ *session-name*\ **"** **-d**

   -  Security cluster (Kerberos authentication enabled)

      -  If the **flink.keystore** and **flink.truststore** file paths are relative paths:

         Run the following command in the directory at the same level as **ssl** to start the session. **ssl/** is a relative path.

         **cd /opt/hadoopclient/Flink/flink/conf/**

         **yarn-session.sh -t ssl/ -nm "**\ *session-name*\ **"** **-d**

         .. code-block::

            ...
            Cluster started: Yarn cluster with application id application_1624937999496_0017
            JobManager Web Interface: http://192.168.1.150:32261

      -  If the **flink.keystore** and **flink.truststore** file paths are absolute paths:

         Run the following command to start a session:

         **cd /opt/hadoopclient/Flink/flink/conf/**

         **yarn-session.sh -nm "**\ *session-name*\ **"** **-d**

#. For a security cluster, run the following command to perform user authentication. If Kerberos authentication is not enabled for the current cluster, you do not need to run this command.

   **kinit** *Username*

#. Explicitly add the OBS file system to be accessed in the Flink command line.

   **echo -e 'test' >/tmp/test**

   **hdfs dfs -mkdir -p obs://**\ *Parallel file system name*\ **/tmp/flinkjob**

   **hdfs dfs -put /tmp/test/ obs://**\ *Parallel file system name*\ **/tmp/flinkjob/**

   **flink run** Client installation directory\ **/Flink/flink/examples/batch/WordCount.jar -input obs://**\ *Parallel file system name*\ **/tmp/flinkjob/test -output obs://**\ *Parallel file system name*\ **/tmp/flinkjob/output**

.. note::

   -  Flink jobs are running on Yarn. Before configuring Flink to interconnect with the OBS file system, ensure that the interconnection between Yarn and the OBS file system is normal.
   -  *Name of the OBS parallel file system/File name*: The OBS file path must be written to the directory level.
   -  If Kerberos authentication has been enabled (security mode) for the cluster, grant the **Read** and **Write** permissions on OBS paths to component users in Ranger by referring to :ref:`Ranger Permission Configuration <mrs_01_248991__en-us_topic_0000001656985534_section116361330121812>`.

.. _mrs_01_248991__en-us_topic_0000001656985534_section116361330121812:

Ranger Permission Configuration
-------------------------------

#. Log in to FusionInsight Manager and choose **System** > **Permission** > **User Group**. On the displayed page, click **Create User Group**.

#. .. _mrs_01_248991__en-us_topic_0000001656985534_li55372842617:

   Create a user group without a role, for example, **obs_flink**, and bind the user group to the corresponding user.

#. Log in to the Ranger management page as the **rangeradmin** user.

#. On the home page, click component plug-in name **OBS** in the **EXTERNAL AUTHORIZATION** area.

#. Click **Add New Policy** to add the **Read** and **Write** permissions on OBS paths to the user group created in :ref:`2 <mrs_01_248991__en-us_topic_0000001656985534_li55372842617>`. If there are no OBS paths, create one in advance (wildcard character **\*** is not allowed).

   |image1|

.. |image1| image:: /_static/images/en-us_image_0000002009454277.png
