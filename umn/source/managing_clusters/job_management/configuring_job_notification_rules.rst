:original_name: mrs_01_0762.html

.. _mrs_01_0762:

Configuring Job Notification Rules
==================================

MRS uses SMN to offer a publish/subscribe model to achieve one-to-multiple message subscriptions and notifications in a variety of message types (SMSs and emails). You can configure job notification rules to receive notifications immediately upon a job execution success or failure.

**Procedure**
-------------

#. Log in to the management console.
#. Click **Service List**. Under **Management & Governance**, click **Simple Message Notification**.
#. Create a topic and add subscriptions to the topic. For details, see :ref:`Configuring Message Notification <mrs_01_0062>`.
#. Go to the MRS management console, and click the cluster name to go to the cluster details page.
#. Click the **Alarms** tab, and choose **Notification Rules** > **Add Notification Rule**.
#. Configure a notification rule for sending job execution results to subscribers.

   .. table:: **Table 1** Parameters of adding a notification rule

      +-----------------------------------+----------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                              |
      +===================================+==========================================================================================================+
      | Rule Name                         | User-defined notification rule name. Only digits, letters, hyphens (-), and underscores (_) are allowed. |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------+
      | Message Notification              | If you enable this function, subscription messages will be sent to subscribers.                          |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------+
      | Topic Name                        | Select an existing topic or click **Create Topic** to create a topic.                                    |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------+
      | Notification Type                 | Select **Event**.                                                                                        |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------+
      | Subscription Items                | a. Click |image1| next to **Suggestion**.                                                                |
      |                                   | b. Click |image2| next to **Manager**.                                                                   |
      |                                   | c. Select **Job Running Succeeded** and **Job Running Failed**.                                          |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001349137917.png
.. |image2| image:: /_static/images/en-us_image_0000001349137917.png
