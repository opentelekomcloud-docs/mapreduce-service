:original_name: admin_guide_000182.html

.. _admin_guide_000182:

Configuring Scheduled Backup of Alarm and Audit Information
===========================================================

Scenario
--------

You can modify the configuration file to periodically back up FusionInsight Manager alarm information, FusionInsight Manager audit information, and audit information of all services to the specified storage location.

The backup can be performed using FTP or SFTP. FTP does not encrypt data, which may cause security risks. Therefore, SFTP is recommended.

Procedure
---------

#. Log in to the active management node as user **omm**.

   .. note::

      Perform this operation only on the active management node. Scheduled backup is not supported on the standby management node.

#. Run the following command to switch the directory:

   **cd ${BIGDATA_HOME}/om-server/om/sbin**

#. Run the following command to configure scheduled backup of FusionInsight Manager's alarm and audit information or service audit information:

   **./setNorthBound.sh -t** *Information type* **-i** *Remote server IP address* **-p** *SFTP or FTP port used by the server*\ **-u** *Username* **-d** *Save path* **-c** *Interval (minutes)* **-m** *Number of records in each file* **-s** *Whether to enable backup* **-e** *Protocol*

   Example:

   **./setNorthBound.sh -t alarm -i 10.0.0.10 -p 22** **-u sftpuser -d /tmp/ -c 10 -m 100 -s true -e sftp**

   This script modifies the alarm backup configuration file **alarm_collect_upload.properties**. The file save path is **${BIGDATA_HOME}/om-server/tomcat/webapps/web/WEB-INF/classes/config**.

   **./setNorthBound.sh -t audit -i 10.0.0.10 -p 22 -u sftpuser -d /tmp/ -c 10** **-m 100** **-s true -e sftp**

   This script modifies the audit backup configuration file **audit_collect_upload.properties**. The file save path is **${BIGDATA_HOME}/om-server/tomcat/webapps/web/WEB-INF/classes/config**.

   **./setNorthBound.sh -t service_audit -i 10.0.0.10 -p 22 -u sftpuser -d /tmp/ -c 10** **-m 100** **-s true -e sftp**

   This script modifies the service audit backup configuration file **service_audit_collect_upload.properties**. The file save path is **${BIGDATA_HOME}/om-server/tomcat/webapps/web/WEB-INF/classes/config**.

#. Enter the password as prompted. The password is encrypted and saved in the configuration file.

   .. code-block::

      Please input sftp/ftp server password:

#. Check the configuration result. If the following information is displayed, the configuration is successful. The configuration file will be automatically synchronized to the standby management node.

   .. code-block::

      execute command syncfile successfully.
      Config Succeed.
