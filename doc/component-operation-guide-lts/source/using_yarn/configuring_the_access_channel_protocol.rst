:original_name: mrs_01_0862.html

.. _mrs_01_0862:

Configuring the Access Channel Protocol
=======================================

Scenario
--------

The value of the **yarn.http.policy** parameter must be consistent on both the server and clients. Web UIs on clients will be garbled if an inconsistency exists, for example, the parameter value is **HTTPS_ONLY** on the server but it is left unspecified on a client (the parameter value **HTTP_ONLY** is applied to the client by default). Set the **yarn.http.policy** parameters on the clients and server to prevent garbled characters from being displayed on the clients.

Procedure
---------

#. On Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Yarn** > **Configurations**. On the displayed page, select **All Configurations** and enter **yarn.http.policy**.

   -  In security mode, set this parameter to **HTTPS_ONLY**.
   -  In normal mode, set this parameter to **HTTP_ONLY**.

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to switch to the client installation directory:

   **cd** **/opt/client**

#. Run the following command to edit the **yarn-site.xml** file:

   **vi** **Yarn/config/yarn-site.xml**

   Change the value of **yarn.http.policy**.

   In security mode, set this parameter to **HTTPS_ONLY**.

   In normal mode, set this parameter to **HTTP_ONLY**.

#. Run the **:wq** command to save execution.

#. Restart the client for the settings to take effect.
