:original_name: mrs_03_1217.html

.. _mrs_03_1217:

How Do I Enable the Map Type on ClickHouse?
===========================================

#. Log in to the active Master node as user **root**.

#. Run the following command to modify the **/opt/Bigdata/components/current/ClickHouse/configurations.xml** configuration file to enable user parameter customization:

   **vim /opt/Bigdata/components/current/ClickHouse/configurations.xml**

   Change **hidden** to **advanced**, as shown in the following information in bold. Then save the configuration and exit.

   .. code-block::

      <property type="hidden" scope="all" classification="Customization" classdesc="RESID_CLICKHOUSE_CONF_0056">
              <name>_clickhouse.custom_content.key</name>
              <value>_user-xml-content</value>
      </property>
      <property type="advanced" scope="all" classification="Customization" classdesc="RESID_CLICKHOUSE_CONF_0056">
             <name>_user-xml-content</name>
             <value vType="text" checker="clickhouse.xmlformat">&lt;yandex&gt;&lt;/yandex&gt;</value>
             <description>RESID_CLICKHOUSE_CONF_0025</description>
      </property>

#. Run the following commands to switch to user **omm** and restart the controller service:

   **su - omm**

   **sh /opt/Bigdata/om-server/om/sbin/restart-controller.sh**

#. Log in to FusionInsight Manager, choose **Cluster** > **Services** > **ClickHouse**. On the page that is displayed, click the **Configurations** tab then the **All Configurations** sub-tab. Click **ClickHouseServer(Role)** > **Customization**, and add the following content to the **\_user-xml-content** configuration item in the right pane:

   .. code-block::

      <yandex>
        <profiles>
          <default>
         <allow_experimental_map_type>1</allow_experimental_map_type>
          </default>
        </profiles>
      </yandex>

#. Click **Save**.

#. Choose **Cluster** > **Services** > **ClickHouse**. In the upper right corner, choose **More** > **Restart Service** to restart the ClickHouse service.
