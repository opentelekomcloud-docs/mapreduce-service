:original_name: mrs_01_2395.html

.. _mrs_01_2395:

Setting the ClickHouse Username and Password
============================================

After a ClickHouse cluster is created, you can use the ClickHouse client to connect to the ClickHouse server. The default username is **default**.

This section describes how to set ClickHouse username and password after a ClickHouse cluster is successfully created.

.. note::

   **default** is the default internal user of ClickHouse. It is an administrator user available only in normal mode (kerberos authentication disabled).


Setting the ClickHouse Username and Password
--------------------------------------------

#. Log in to Manager and choose **Cluster** > **Services** > **ClickHouse**. Click the **Configurations** tab and then **All Configurations**.

#. Search for the **users.default.password** parameter in the search box and change its password, as shown in :ref:`Figure 1 <mrs_01_2395__fig42238424419>`.

   .. _mrs_01_2395__fig42238424419:

   .. figure:: /_static/images/en-us_image_0000001296059672.png
      :alt: **Figure 1** Changing the default user password

      **Figure 1** Changing the default user password

#. Log in to the node where the client is installed and run the following command to switch to the client installation directory.

   **cd**\ *Cluster client installation directory*

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Log in to ClickHouse using the new password.

   **clickhouse client --host** *IP address of the ClickHouse instance* **--user** *default* **--password** *xxx*

   .. note::

      To obtain the service IP address of the ClickHouse instance, choose **Components** > **ClickHouse** > **Instances** on the cluster details page.
