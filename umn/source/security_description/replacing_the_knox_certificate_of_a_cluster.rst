:original_name: mrs_01_300854.html

.. _mrs_01_300854:

Replacing the Knox Certificate of a Cluster
===========================================

Scenarios
---------

The certificate for an existing cluster will expire on December 31, 2026. Once the certificate expires, node management operations (such as scaling out or in) and component management functions will become unavailable. If a Knox certificate in a cluster is about to expire, an alert will appear on the cluster dashboard page. Then, replace the certificate by following the subsequent steps.

Notes and Constraints
---------------------

The cluster must be in the **Running** state, and both the active and standby OMS nodes must also be in the **Running** state.

Impact on the System
--------------------

-  Updating the certificate restarts active and standby OMS nodes, which may temporarily disrupt management plane services. Before updating the certificate, ensure no scheduled auto scaling or manual scaling operations are running on the management plane. Job submissions through the client are not affected.
-  During the certificate update, cluster nodes are automatically authorized for one hour. Once the update is complete, this authorization is automatically revoked.

Procedure
---------

#. Log in to the MRS console.

#. On the **Active Clusters** page, select a running target cluster and click its name to go to the cluster details page.

#. Click **Update now** in the certificate update alert.

   |image1|

#. Select the check box in the dialog box and click **OK** to update the certificate.

   |image2|

#. If the certificate update fails, view the error details on the cluster **Dashboard** page. If the certificate update still fails after you retry based on the error message, contact O&M personnel for troubleshooting.

Verifying the Certificate Replacement
-------------------------------------

**Method 1:**

Log in to the MRS console, click **Operation Logs**, and check the logs to verify that the certificate updated successfully.

|image3|

**Method 2:**

Log in to MRS Manager, press **F12** to open Developer Tools, select the **Security** tab, and click **View certificate** to verify that the certificate validity period is 100 years.

|image4|

.. |image1| image:: /_static/images/en-us_image_0000002772366042.png
.. |image2| image:: /_static/images/en-us_image_0000002801766049.png
.. |image3| image:: /_static/images/en-us_image_0000002801766113.png
.. |image4| image:: /_static/images/en-us_image_0000002801606657.png
