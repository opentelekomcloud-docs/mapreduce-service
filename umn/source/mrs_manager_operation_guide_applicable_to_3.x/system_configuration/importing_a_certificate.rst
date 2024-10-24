:original_name: admin_guide_000157.html

.. _admin_guide_000157:

Importing a Certificate
=======================

Scenario
--------

CA certificates are used to encrypt data during communication between MRS Manager modules and between cluster component clients and servers to ensure security. CA certificates can be quickly imported to MRS Manager for product security. Import CA certificates in following scenarios:

-  When the cluster is installed for the first time, you need to replace the enterprise certificate.
-  If the enterprise certificate has expired or security hardening is required, you need to replace it with a new certificate.

Impact on the System
--------------------

-  During certificate replacement, the cluster needs to be restarted. In this case, the system becomes inaccessible and cannot provide services.
-  After the certificate is replaced, the certificates used by all components and MRS Manager modules are automatically updated.
-  After the certificate is replaced, you need to reinstall the certificate in the local environment where the certificate is not trusted.

Prerequisites
-------------

-  You have generated the certificate file and key file or obtained them from the enterprise certificate administrator.

-  You have obtained the files to be imported to the cluster, including the CA certificate file (**\*.crt**), key file (**\*.key**), and file that saves the key file password (**password.property**). The certificate name and key name can contain uppercase letters, lowercase letters, and digits. After the preceding files are generated, compress them into a TAR package.

-  You have obtained a password for accessing the key file, for example, **Userpwd@123**.

   To avoid potential security risks, the password must meet the following complexity requirements:

   -  It must contain at least eight characters.
   -  It must contain at least four of the following character types: uppercase letters, lowercase letters, digits, and special characters :literal:`~`!?,.:;-_'(){}[]/<>@#$%^&*+|\\=.`

-  When applying for certificates from the certificate administrator, you have provided the password for accessing the key file and applied for the certificate files in CRT, CER, CERT, and PEM formats and the key files in KEY and PEM formats. The requested certificates must have the issuing function.

Procedure
---------

#. Log in to MRS Manager and choose **System** > **Certificate**.

#. Click |image1| on the right of **Upload Certificate**. In the file selection window, browse to select the obtained TAR package of the certificate files.

#. Click **Upload**.

   Manager uploads the compressed package and automatically imports the package.

#. After the certificate is imported, the system displays a message asking you to synchronize the cluster configuration and restart the web service for the new certificate to take effect. Click **OK**.

#. In the displayed dialog box, enter the password of the current login user and click **OK**. The cluster configuration is automatically synchronized and the web service is restarted.

#. After the cluster is restarted, enter the URL for accessing MRS Manager in the address box of the browser and check whether the MRS Manager web page can be successfully displayed.

#. Log in to MRS Manager.

#. Choose **Cluster**, click the name of the target cluster, choose **Dashboard**, click **More**, and select **Restart**. (For MRS 3.3.0 or later, choose **More** > **Restart** in the upper right corner of the home page.)

#. In the displayed dialog box, enter the password of the current login user and click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001392574046.png
