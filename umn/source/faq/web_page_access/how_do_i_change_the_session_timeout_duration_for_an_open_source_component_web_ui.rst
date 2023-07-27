:original_name: mrs_03_1151.html

.. _mrs_03_1151:

How Do I Change the Session Timeout Duration for an Open Source Component Web UI?
=================================================================================

You need to set a proper web session timeout duration for security purposes. To change the session timeout duration, do as follows:

Checking Whether the Cluster Supports Session Timeout Duration Adjustment
-------------------------------------------------------------------------

-  For MRS cluster versions earlier than 3.x:

   #. On the cluster details page, choose **Components** > **meta** > **Service Configuration**.

   #. Switch **Basic** to **All**, and search for the **http.server.session.timeout.secs**.

      If **http.server.session.timeout.secs** does not exist, the cluster does not support change of the session timeout duration. If the parameter exists, perform the following steps to modify it.

-  MRS 3.x and later: Log in to FusionInsight Manager and choose **Cluster** > **Services** > **meta**. On the displayed page, click **Configurations** and select **All Configurations**. Search for the **http.server.session.timeout.secs** configuration item. If this configuration item exists, perform the following steps to modify it. If the configuration item does not exist, the version does not support dynamic adjustment of the session duration.

   |image1|

You are advised to set all session timeout durations to the same value. Otherwise, the settings of some parameters may not take effect due to value conflict.

Modifying the Timeout Duration on Manager and the Authentication Center Page
----------------------------------------------------------------------------

**For clusters of versions earlier than MRS 3.\ x:**

#. Log in to each master node in the cluster and perform :ref:`2 <mrs_03_1151__li11295622161919>` to :ref:`4 <mrs_03_1151__li629512210191>`.

#. .. _mrs_03_1151__li11295622161919:

   Change the value of **<session-timeout>20</session-timeout>** in the **/opt/Bigdata/apache-tomcat-7.0.78/webapps/cas/WEB-INF/web.xml** file. **<session-timeout>20</session-timeout>** indicates the session timeout duration, in minutes. Change it based on service requirements. The maximum value is 480 minutes.

#. Change the value of **<session-timeout>20</session-timeout>** in the **/opt/Bigdata/apache-tomcat-7.0.78/webapps/web/WEB-INF/web.xml** file. **<session-timeout>20</session-timeout>** indicates the session timeout duration, in minutes. Change it based on service requirements. The maximum value is 480 minutes.

#. .. _mrs_03_1151__li629512210191:

   Change the values of **p:maxTimeToLiveInSeconds="${tgt.maxTimeToLiveInSeconds:1200}"** and **p:timeToKillInSeconds="${tgt.timeToKillInSeconds:1200}"** in the **/opt/Bigdata/apache-tomcat-7.0.78/webapps/cas/WEB-INF/spring-configuration/ticketExpirationPolicies.xml** file. The maximum value is 28,800 seconds.

#. Restart the Tomcat node on the active master node.

   a. .. _mrs_03_1151__li11295192217194:

      On the active master node, run the **netstat -anp \|grep 28443 \|grep LISTEN \| awk '{print $7}'** command as user **omm** to query the Tomcat process ID.

   b. Run the **kill -9** *{pid}* command, in which *{pid}* indicates the Tomcat process ID obtained in :ref:`5.a <mrs_03_1151__li11295192217194>`.

   c. Wait until the process automatically restarts. You can run the **netstat -anp \|grep 28443 \|grep LISTEN** command to check whether the process is successfully restarted. If the process can be queried, the process is successfully restarted. If the process cannot be queried, query the process again later.

**For clusters of MRS 3.\ x** **or later**

#. Log in to each master node in the cluster and perform :ref:`2 <mrs_03_1151__li388340175410>` to :ref:`3 <mrs_03_1151__li10492102775910>` on each master node.

#. .. _mrs_03_1151__li388340175410:

   Change the value of **<session-timeout>20</session-timeout>** in the **/opt/Bigdata/om-server_xxx/apache-tomcat-xxx/webapps/web/WEB-INF/web.xml** file. **<session-timeout>20</session-timeout>** indicates the session timeout duration, in minutes. Change it based on service requirements. The maximum value is 480 minutes.

#. .. _mrs_03_1151__li10492102775910:

   Add **ticket.tgt.timeToKillInSeconds=28800** to the **/opt/Bigdata/om-server_xxx/apache-tomcat-8.5.63/webapps/cas/WEB-INF/classes/config/application.properties** file. **ticket.tgt.timeToKillInSeconds** indicates the validity period of the authentication center, in seconds. Change it based on service requirements. The maximum value is 28,800 seconds.

#. Restart the Tomcat node on the active master node.

   a. .. _mrs_03_1151__li145761437910:

      On the active master node, run the **netstat -anp \|grep 28443 \|grep LISTEN \| awk '{print $7}'** command as user **omm** to query the Tomcat process ID.

   b. Run the **kill -9** *{pid}* command, in which *{pid}* indicates the Tomcat process ID obtained in :ref:`4.a <mrs_03_1151__li145761437910>`.

   c. Wait until the process automatically restarts.

      You can run the **netstat -anp \|grep 28443 \|grep LISTEN** command to check whether the process is successfully restarted. If the process is displayed, the process is successfully restarted. If the process is not displayed, query the process again later.

Modifying the Timeout Duration for an Open-Source Component Web UI
------------------------------------------------------------------

#. Access the **All Configurations** page.

   -  For MRS cluster versions earlier than MRS 3.x:

      On the cluster details page, choose **Components > Meta > Service Configuration**.

   -  For MRS cluster version 3.\ *x* or later:

      Log in to FusionInsight Manager and choose **Cluster** > **Services** > **meta**. On the displayed page, click **Configurations** and select **All Configurations**.

#. Change the value of **http.server.session.timeout.secs** under **meta** as required. The unit is second.

#. Save the settings, deselect **Restart the affected services or instances**, and click **OK**.

   You are advised to perform the restart during off-peak hours.

#. (Optional) If you need to use the Spark web UI, search for **spark.session.maxAge** on the **All Configurations** page of Spark and change the value (in seconds).

   Save the settings, deselect **Restart the affected services or instances**, and click **OK**.

#. Restart the meta service and components on web UI, or restart the cluster during off-peak hours.

   To prevent service interruption, restart the service during off-peak hours or perform a rolling restart.

.. |image1| image:: /_static/images/en-us_image_0000001392734334.png
