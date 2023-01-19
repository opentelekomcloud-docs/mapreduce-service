:original_name: mrs_01_1032.html

.. _mrs_01_1032:

Creating a Kafka Role
=====================

Scenario
--------

This section describes how to create and configure a Kafka role.

.. note::

   Users can create Kafka roles only in security mode.

   If the current component uses Ranger for permission control, you need to configure permission management policies based on Ranger. For details, see :ref:`Adding a Ranger Access Permission Policy for Kafka <mrs_01_1861>`.

Prerequisites
-------------

The system administrator has understood the service requirements.

Procedure
---------

#. Log in to FusionInsight Manager and choose **System** > **Permission** > **Role**.

#. On the displayed page, click **Create Role** and enter a **Role Name** and **Description**.

#. On the **Configure Resource Permission** page, choose *Name of the desired cluster* > **Kafka**.

#. Select permissions based on service requirements. For details about configuration items, see :ref:`Table 1 <mrs_01_1032__en-us_topic_0000001173949236_table25376475282>`.

   .. _mrs_01_1032__en-us_topic_0000001173949236_table25376475282:

   .. table:: **Table 1** Description

      +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Scenario                                                | Role Authorization                                                                                                                                      |
      +=========================================================+=========================================================================================================================================================+
      | Setting the Kafka administrator permissions             | In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Kafka** > **Kafka Manager Privileges**.                        |
      |                                                         |                                                                                                                                                         |
      |                                                         | .. note::                                                                                                                                               |
      |                                                         |                                                                                                                                                         |
      |                                                         |    This permission allows you to create and delete topics, but does not allow you to produce or consume any topics.                                     |
      +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Setting the production permission of a user on a topic  | a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Kafka** > **Kafka Topic Producer And Consumer Privileges**. |
      |                                                         | b. In the **Permission** column of the specified topic, select **Kafka Producer Permission**.                                                           |
      +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Setting the consumption permission of a user on a topic | a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Kafka** > **Kafka Topic Producer And Consumer Privileges**. |
      |                                                         | b. In the **Permission** column of the specified topic, select **Kafka Consumer Privileges**.                                                           |
      +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**, and return to the **Role** page.
