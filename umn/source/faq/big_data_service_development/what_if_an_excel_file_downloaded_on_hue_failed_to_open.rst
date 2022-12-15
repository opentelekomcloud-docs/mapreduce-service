:original_name: mrs_03_1160.html

.. _mrs_03_1160:

What If an Excel File Downloaded on Hue Failed to Open?
=======================================================

.. note::

   This section applies only to versions earlier than MRS 3.\ *x*.

#. Log in to a Master node as user **root** and switch to user **omm**.

   **su - omm**

#. Check whether the current node is the active OMS node.

   **sh ${BIGDATA_HOME}/om-0.0.1/sbin/status-oms.sh**

   If **active** is displayed in the command output, the node is the active node. Otherwise, log in to the other Master node.


   .. figure:: /_static/images/en-us_image_0000001439442217.png
      :alt: **Figure 1** Active OMS node

      **Figure 1** Active OMS node

#. Go to the **{BIGDATA_HOME}/Apache-httpd-*/conf** directory.

   **cd ${BIGDATA_HOME}/Apache-httpd-*/conf**

#. Open the **httpd.conf** file.

   **vim httpd.conf**

#. Search for **21201** in the file and delete the following content from the file. (The values of *proxy_ip* and *proxy_port* are the same as those in the actual environment.)

   .. code-block::

      ProxyHTMLEnable On
      SetEnv PROXY_PREFIX=https://[proxy_ip]:[proxy_port]
      ProxyHTMLURLMap (https?:\/\/[^:]*:[0-9]*.*) ${PROXY_PREFIX}/proxyRedirect=$1 RV


   .. figure:: /_static/images/en-us_image_0268284607.png
      :alt: **Figure 2** Content to be deleted

      **Figure 2** Content to be deleted

#. Save the modification and exit.

#. Open the **httpd.conf** file again, search for **proxy_hue_port**, and delete the following content:

   .. code-block::

      ProxyHTMLEnable On
      SetEnv PROXY_PREFIX=https://[proxy_ip]:[proxy_port]
      ProxyHTMLURLMap (https?:\/\/[^:]*:[0-9]*.*) ${PROXY_PREFIX}/proxyRedirect=$1 RV


   .. figure:: /_static/images/en-us_image_0268298534.png
      :alt: **Figure 3** Content to be deleted

      **Figure 3** Content to be deleted

#. Save the modification and exit.

#. Run the following command to restart the **httpd** process:

   **sh ${BIGDATA_HOME}/Apache-httpd-\*/setup/restarthttpd.sh**

#. Check whether the **httpd.conf** file on the standby Master node is modified. If the file is modified, no further action is required. If the file is not modified, modify the **httpd.conf** file on the standby Master node in the same way. You do not need to restart the **httpd** process.

#. Download the Excel file again. You can open the file successfully.
