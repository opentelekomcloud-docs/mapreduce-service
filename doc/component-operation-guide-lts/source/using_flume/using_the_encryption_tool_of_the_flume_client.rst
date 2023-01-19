:original_name: mrs_01_0395.html

.. _mrs_01_0395:

Using the Encryption Tool of the Flume Client
=============================================

Scenario
--------

You can use the encryption tool provided by the Flume client to encrypt some parameter values in the configuration file.

Prerequisites
-------------

The Flume client has been installed.

Procedure
---------

#. Log in to the Flume client node and go to the client installation directory, for example, **/opt/FlumeClient**.

#. Run the following command to switch the directory:

   **cd fusioninsight-flume-**\ *Flume component version number*\ **/bin**

#. Run the following command to encrypt information:

   **./genPwFile.sh**

   Input the information that you want to encrypt twice.

#. Run the following command to query the encrypted information:

   **cat password.property**

   .. note::

      If the encryption parameter is used for the Flume server, you need to perform encryption on the corresponding Flume server node. You need to run the encryption script as user **omm** for encryption.
