:original_name: mrs_01_248995.html

.. _mrs_01_248995:

Interconnecting HetuEngine with OBS
===================================

Interconnecting with OBS
------------------------

In an MRS cluster, **Location** can be set to an OBS file system path during HetuEngine table creation and HetuEngine can connect to OBS through Hive Metastore.

-  Setting **Location** to the OBS file system path when creating a table

   #. If a HetuEngine compute instance is running, restart it.

      Log in to FusionInsight Manager as a user who has permission to access the HetuEngine web UI. Choose **Cluster** > **Services** > **HetuEngine**. In the **Basic Information** area in the Dashboard tab, click the link next to **HSConsole WebUI**. On the displayed HSConsole page, click **Compute Instance**. In the instance list, click **Restart** in the **Operation** column and operate as prompted.

   #. Log in to the node where the HetuEngine service client is located as the client installation user and run the following command:

      **source** *Client installation directory*\ **/bigdata_env**

   #. Log in to the HetuEngine client based on the cluster authentication mode.

      -  Kerberos authentication has been enabled for the cluster (security mode): Run the following command to complete user authentication and log in to the HetuEngine client:

         **kinit** *User performing HetuEngine operations*

         **hetu-cli --catalog hive --tenant default --schema default**

         For details about how to assign permissions to users in the Ranger, see :ref:`Configuring Ranger Permissions <mrs_01_248995__en-us_topic_0000001705304945_section116361330121812>`.

      -  Kerberos authentication is not enabled for the cluster (normal mode): Run the following command to log in to the HetuEngine client:

         **hetu-cli --catalog hive --tenant default --schema default --user** *User performing HetuEngine operations*

   #. Set **Location** to the OBS file system path when creating a table.

      **create table test(name string) with (location = 'obs://**\ *Name of the OBS parallel file system*\ **/user/hive/warehouse/test');**

-  Interconnecting with OBS through Hive Metastore

   #. Complete the configurations by referring to :ref:`Interconnecting Hive with OBS using MetaStore <mrs_01_248989__en-us_topic_0000001656985526_section18127143141811>`.
   #. Log in to FusionInsight Manager, choose **Cluster** > **Services** > **HetuEngine**. On the displayed page, choose **More** > **Synchronize Configuration**. After the synchronization is complete, choose **More** > **Synchronize Configuration** again and then restart the HetuEngine service as prompted.

      .. important::

         If a HetuEngine compute instance is running, stop it before restarting the service. After the service is restarted, start this compute instance.

   #. No location needs to be specified when you log in to the HetuEngine client to create a schema or table. The schema or table is stored on OBS by default.

.. _mrs_01_248995__en-us_topic_0000001705304945_section116361330121812:

Configuring Ranger Permissions
------------------------------

For HetuEngine clusters with Kerberos authentication enabled (security mode), the methods to grant Ranger permission are the same for both storage-compute decoupled architecture and and storage-compute coupled architecture.
