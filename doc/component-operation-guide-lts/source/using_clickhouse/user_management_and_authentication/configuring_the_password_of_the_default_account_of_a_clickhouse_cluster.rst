:original_name: mrs_01_24575.html

.. _mrs_01_24575:

Configuring the Password of the Default Account of a ClickHouse Cluster
=======================================================================

After a ClickHouse cluster is created, you can use the ClickHouse client to connect to the ClickHouse server.

Configure the passwords of the default accounts **default** and **clickhouse** of a ClickHouse cluster.

.. note::

   -  This section applies to MRS 3.2.0 or later.
   -  **default** and **clickhouse** is the default internal administrator of a ClickHouse cluster in normal mode (with Kerberos authentication disabled).


Configuring the Password of the Default Account of a ClickHouse Cluster
-----------------------------------------------------------------------

#. Install the ClickHouse client.

#. Log in to the ClickHouse client node as user **root**, go to *Client installation directory*\ **/ClickHouse/clickhouse/config**, and check whether the **metrika.xml** file contains information about all ClickHouseServer nodes. If information of any nodes is missing, add it.

   For example, there are four ClickHouseServer nodes: **192-168-43-125**, **192-168-43-165**, **192-168-43-175**, and **192-168-43-249**.

   .. code-block::

      <shard>
              <internal_replication>true</internal_replication>
              <replica>
                <host>192-168-43-125</host>
                <port>21423</port>
                <user>clickhouse</user>
                <password/>
              </replica>
              <replica>
                <host>192-168-43-165</host>
                <port>21423</port>
                <user>clickhouse</user>
                <password/>
              </replica>
            </shard>
            <shard>
              <internal_replication>true</internal_replication>
              <replica>
                <host>192-168-43-175</host>
                <port>21423</port>
                <user>clickhouse</user>
                <password/>
              </replica>
              <replica>
                <host>192-168-43-249</host>
                <port>21423</port>
                <user>clickhouse</user>
                <password/>
              </replica>
            </shard>

#. Go to *Client installation directory*\ **/ClickHouse/clickhouse/config** and check whether the values of **CLICKHOUSE_CONF_DIR** and **CLICKHOUSE_INSTALL_HOME** in the **clickhouse-env.sh** file is **$BIGDATA_HOME/FusionInsight_ClickHouse_xxx/*_ClickHouseServer/etc** and **$BIGDATA_HOME/FusionInsight_ClickHouse_xxx/install/FusionInsight-ClickHouse-*-lts/**, respectively.

   |image1|

#. Switch to user **omm** and go to the *Client installation directory*\ **/ClickHouse/clickhouse_change_password** directory.

   **su - omm**

   **cd** *Client installation directory*\ **/ClickHouse/clickhouse_change_password**

#. Run the following command to change the password of the **default** or **clickhouse** user:

   **./change_password.sh**

   In the following figure, user **clickhouse** is used as an example. Enter **clickhouse** and its password as prompted, and wait until the password is changed.

   |image2|

   .. note::

      The password complexity requirements are as follows:

      -  The password contains 8 to 64 characters.
      -  The password must contain at least one lowercase letter, one uppercase letter, one digit, and one special character, and the following special characters are supported: ``-%;[]{}@_``

#. Check the password change result.

   a. Run the following commands to check the value of **CLICKHOUSE_CONF_DIR** in the *Client installation directory*\ **/ClickHouse/clickhouse/config/clickhouse-env.sh** file:

      **cd** *Client installation directory*\ **/ClickHouse/clickhouse/config/**

      **vi clickhouse-env.sh**

      The following is an example:

      .. code-block::

         LICKHOUSE_CONF_DIR="${BIGDATA_HOME}/FusionInsight_ClickHouse_*/*_ClickHouseServer/etc"
         CLICKHOUSE_SECURITY_ENABLED="true"
         CLICKHOUSE_BALANCER_LIST="192.168.42.14,192.168.67.89"
         CLICKHOUSE_STARTUP_PRINCIPAL="clickhouse/hadoop.hadoop.com@HADOOP.COM"
         USER_REALM="HADOOP.COM"
         OM_DECOMMISSION_HOSTNAME_LIST=""
         CLICKHOUSE_INSTALL_HOME="${BIGDATA_HOME}/FusionInsight_ClickHouse_8.2.0/install/FusionInsight-ClickHouse-v22.3.2.2-lts"
         CK_BALANCER_LIST="server-2110081635-0003,server-2110082001-0019"

   b. Log in to the ClickHouse Server node and check the value of **password_sha256_hex** in the **${BIGDATA_HOME}/FusionInsight_ClickHouse_*/*_ClickHouseServer/etc/users.xml** file. The value is the new password.

      **cd ${BIGDATA_HOME}/**\ ``FusionInsight_ClickHouse_*``\ **/**\ ``*_ClickHouseServer``\ **/etc/**

      **vi** **users.xml**

      As shown in the following figure, the new password is stored in the **password_sha256_hex** file.

      |image3|

.. |image1| image:: /_static/images/en-us_image_0000001583316949.png
.. |image2| image:: /_static/images/en-us_image_0000001532677010.png
.. |image3| image:: /_static/images/en-us_image_0000001583436657.png
