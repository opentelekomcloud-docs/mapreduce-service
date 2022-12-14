:original_name: mrs_01_0764.html

.. _mrs_01_0764:

Accessing the Ranger Web UI and Synchronizing Unix Users to the Ranger Web UI
=============================================================================

You can manage Ranger on the Ranger web UI.

Accessing the Ranger Admin Web UI
---------------------------------

#. On the MRS management console, click the cluster name to go to the cluster details page.

#. Click the **Components** tab.

#. Select **Ranger**. In **Ranger Summary**, click **RangerAdmin** corresponding to **Ranger Web UI**.

#. On the Ranger web UI login page, the default username for MRS 1.9.2 is **admin** and the password is **admin@12345**. The default username for MRS 1.9.3 is **admin** and the password is **ranger@A1!**.

   After logging in to the Ranger Web UI for the first time, change the password and keep it secure.

#. Click the username in the upper right corner, choose **Profile** from the drop-down list, and click **Change Password** to change the password.


   .. figure:: /_static/images/en-us_image_0000001438507709.png
      :alt: **Figure 1** Changing the Ranger web UI login password

      **Figure 1** Changing the Ranger web UI login password

#. After changing the password, click the username in the upper right corner, choose **Log Out** from the drop-down list, and use the new password to log in to the web UI again.

Using Ranger UserSync to Synchronize Unix OS Users on Cluster Nodes
-------------------------------------------------------------------

Ranger UserSync is an important component of Ranger. It can synchronize Unix system users or LDAP users to the Ranger web UI. Currently, MRS can synchronize only Unix users on the node where the Ranger UserSync process resides.

#. Log in to the node where the Ranger UserSync process is located.

#. Run the **useradd** command to add a system user, for example, **testuser**.


   .. figure:: /_static/images/en-us_image_0000001348770621.png
      :alt: **Figure 2** Adding the **testuser** system user

      **Figure 2** Adding the **testuser** system user

#. After the user is added, wait for about 1 minute and log in to the Ranger web UI. Then, you can see that the user is synchronized.


   .. figure:: /_static/images/en-us_image_0000001438508081.png
      :alt: **Figure 3** User synchronization completed

      **Figure 3** User synchronization completed
