:original_name: mrs_01_0786.html

.. _mrs_01_0786:

Communication Security Authorization
====================================

MRS clusters provision, manage, and use big data components through the management console. Big data components are deployed in a user's VPC. If the MRS management console needs to directly access big data components deployed in the user's VPC, you need to enable the corresponding security group rules after you have obtained user authorization. This authorization process is called secure communications.

If the secure communications function is not enabled, MRS clusters cannot be created. If you disable the communication after a cluster is created, the cluster status will be **Network channel is not authorized** and the following functions will be affected:

-  Functions, such as big data component installation, cluster scale-out/scale-in, and Master node specification upgrade, are unavailable.
-  The cluster running status, alarms, and events cannot be monitored.
-  The node management, component management, alarm management, file management, job management, patch management, and tenant management functions on the cluster details page are unavailable.
-  The Manager page and the website of each component cannot be accessed.

After the secure communications function is enabled again, the cluster status is restored to **Running**, and the preceding functions become available. For details, see :ref:`Enabling Secure Communications for Clusters with This Function Disabled <mrs_01_0786__section177319347305>`.

If the security group rules authorized in the cluster are insufficient for you to provision, manage, and use big data components, |image1| is displayed on the right of **Secure Communications**. In this case, click **Update** to update the security group rules. For details, see :ref:`Update <mrs_01_0786__section171375139619>`.

Enabling Secure Communications During Cluster Creation
------------------------------------------------------

#. Log in to the MRS console.

#. Click Create **Cluster**. The corresponding page is displayed.

#. Click **Quick Config** or **Custom Config**.

#. Configure cluster information by referring to :ref:`Creating a Custom Cluster <mrs_01_0513>`.

#. In the **Secure Communications** area of the **Advanced Settings** tab page, select **Enable**.

#. Click **Create** **Now**.

   If Kerberos authentication is enabled for a cluster, check whether Kerberos authentication is required. If yes, click **Continue**. If no, click **Back** to disable Kerberos authentication and then create a cluster.

Disabling Secure Communications After a Cluster Is Created
----------------------------------------------------------

#. Log in to the MRS console.

#. In the active cluster list, click the name of the cluster for which you want to disable secure communications.

   The cluster details page is displayed.

#. Click the switch on the right of **Secure Communications** to disable authorization. In the dialog box that is displayed, click **OK**.

   After the authorization is disabled, the cluster status changes to **Network channel unauthorized**, and some functions of the cluster are unavailable. Exercise caution when performing this operation.

.. _mrs_01_0786__section177319347305:

Enabling Secure Communications for Clusters with This Function Disabled
-----------------------------------------------------------------------

#. Log in to the MRS console.

#. In the active cluster list, click the name of the cluster for which you want to enable secure communications.

   The cluster details page is displayed.

#. Click the switch on the right of **Secure Communications** to enable the function.

   After the function is enabled, the cluster status changes to **Running**.

.. _mrs_01_0786__section171375139619:

Update
------

If the security group rules authorized in the cluster are insufficient for you to provision, manage, and use big data components, |image2| is displayed on the right of **Secure Communications**. In this case, click **Update** to update the security group rules. For details, see :ref:`Update <mrs_01_0786__section171375139619>`.

#. Log in to the MRS console.

#. In the active cluster list, click the name of the cluster for which you want to update secure communications.

   The cluster details page is displayed.

#. Click **Update** on the right of **Secure Communications**.


   .. figure:: /_static/images/en-us_image_0000001349257145.png
      :alt: **Figure 1** Update

      **Figure 1** Update

#. Click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001349137565.png
.. |image2| image:: /_static/images/en-us_image_0000001296057856.png
