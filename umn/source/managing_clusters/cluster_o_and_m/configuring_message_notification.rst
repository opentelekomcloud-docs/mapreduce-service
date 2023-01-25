:original_name: mrs_01_0062.html

.. _mrs_01_0062:

Configuring Message Notification
================================

MRS uses SMN to offer a publish/subscribe model to achieve one-to-multiple message subscriptions and notifications in a variety of message types (SMSs and emails).

Scenario
--------

On the MRS management console, you can enable or disable the notification service on the **Alarms** page. The functions in the following scenarios can be implemented only after the required cluster function is enabled:

-  After a user subscribes to the notification service, the MRS management plane notifies the user of success or failure of manual cluster scale-out and scale-in, cluster termination, and auto scaling by emails or SMS messages.
-  The management plane checks the alarms about the MRS cluster and sends a notification to the tenant if the alarms are critical.
-  If either of the operations such as deletion, shutdown, specifications modification, restart, and OS update is performed on an ECS in a cluster, the MRS cluster works abnormally. The management plane notifies a user when detecting that the VM of the user is in either of the preceding operations.

Creating a Topic
----------------

A topic is a specified event for message publication and notification subscription. It serves as a message sending channel, where publishers and subscribers can interact with each other.

#. Log in to the management console.

#. Click **Service List**. Under **Management & Governance**, click **Simple Message Notification**.

   The **SMN** page is displayed.

#. In the navigation pane, choose **Topic Management** > **Topics**.

   The **Topics** page is displayed.

#. Click **Create Topic**.

   The **Create Topic** dialog box is displayed.

#. In **Topic Name**, enter a topic name. In **Display Name**, enter a display name.

#. Select an existing project from the **Enterprise Project** drop-down list, or click **Create Enterprise Project** to create an enterprise project on the **Enterprise Project Management** page and then select it.

#. Set tag keys and tag values. Tags consist of keys and values. They identify cloud resources so that you can easily categorize and search for your resources.

.. _mrs_01_0062__section186691424145018:

Adding Subscriptions to a Topic
-------------------------------

To deliver messages published to a topic to subscribers, you must add subscription endpoints to the topic. SMN automatically sends a confirmation message to the subscription endpoint. The confirmation message is valid only within 48 hours. The subscribers must confirm the subscription within 48 hours so that they can receive notification messages. Otherwise, the confirmation message becomes invalid, and you need to send it again.

#. Log in to the management console.

#. Under **Management & Governance**, click **Simple Message Notification**.

   The **SMN** page is displayed.

#. In the navigation pane, choose **Topic Management** > **Topics**.

   The **Topics** page is displayed.

#. Locate the topic to which you want to add a subscription, click **More** in the **Operation** column, and select **Add Subscription**.

   The **Add Subscription** box is displayed.

   Protocol can be set to **SMS**, FunctionGraph (function), **HTTP**, **HTTPS**, and **Email**.

   **Endpoint** indicates the address of the subscription endpoint. SMS and email, endpoints can be entered in batches. When adding endpoints in batches, each endpoint address occupies a line. You can enter a maximum of 10 endpoints.

5. Click **OK**.

The subscription you added is displayed in the subscription list.

Sending Notifications to Subscribers
------------------------------------

#. Log in to the MRS console.
#. Click |image1| in the upper-left corner on the management console and select a region and project.
#. Choose **Clusters > Active Clusters**, select a running cluster, and click its name to switch to the cluster details page.
#. Click **Alarms**.
#. Choose **Notification Rules** > **Add Notification Rule**. The **Add Notification Rule** page is displayed.
#. Set the notification rule parameters.

   .. table:: **Table 1** Parameters of a notification rule

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                         |
      +===================================+=====================================================================================================================+
      | Rule Name                         | User-defined notification rule name. Only digits, letters, hyphens (-), and underscores (_) are allowed.            |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------+
      | Message Notification              | -  If you enable this function, the system sends notifications to subscribers based on the notification rule.       |
      |                                   | -  If you disable this function, the rule does not take effect, that is, notifications are not sent to subscribers. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------+
      | Topic Name                        | Select an existing topic or click **Create Topic** to create a topic.                                               |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------+
      | Notification Type                 | Select the type of the notification to be subscribed to.                                                            |
      |                                   |                                                                                                                     |
      |                                   | -  Alarm                                                                                                            |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------+
      | Subscription Items                | Select the items to be subscribed to. You can select all or some items as required.                                 |
      |                                   |                                                                                                                     |
      |                                   | Subscription rules in MRS 3.\ *x* or later:                                                                         |
      |                                   |                                                                                                                     |
      |                                   | Alarm severity: critical, major, and minor                                                                          |
      |                                   |                                                                                                                     |
      |                                   | Subscription rules in versions earlier than MRS 3.x:                                                                |
      |                                   |                                                                                                                     |
      |                                   | -  Critical                                                                                                         |
      |                                   | -  Major                                                                                                            |
      |                                   | -  Minor                                                                                                            |
      |                                   | -  Suggestion                                                                                                       |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001295898140.png
