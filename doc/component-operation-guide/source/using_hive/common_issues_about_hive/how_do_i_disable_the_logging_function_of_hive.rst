:original_name: mrs_01_24482.html

.. _mrs_01_24482:

How Do I Disable the Logging Function of Hive?
==============================================

Question
--------

How do I disable the logging function of Hive?

Answer
------

#. Log in to the node where the client is installed as user **root**.

#. Run the following command to switch to the client installation directory, for example, **/opt/Bigdata/client**:

   **cd** **/opt/Bigdata/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Log in to the Hive client based on the cluster authentication mode.

   -  In security mode, run the following command to complete user authentication and log in to the Hive client:

      **kinit** *Component service user*

      **beeline**

   -  In normal mode, run the following command to log in to the Hive client:

      -  Run the following command to log in to the Hive client as the component service user:

         **beeline -n** *component service user*

      -  If no component service user is specified, the current OS user is used to log in to the Hive client.

         **beeline**

#. Run the following command to disable the logging function:

   **set hive.server2.logging.operation.enabled=false;**

#. Run the following command to check whether the logging function is disabled. If the following information is displayed, the logging function is disabled successfully.

   **set hive.server2.logging.operation.enabled;**

   |image1|

.. |image1| image:: /_static/images/en-us_image_0000001296250116.png
