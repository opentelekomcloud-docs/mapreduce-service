:original_name: mrs_01_2321.html

.. _mrs_01_2321:

How Do I Perform Operations After the Domain Name Is Changed?
=============================================================

Question
--------

After the domain name is changed, the installed client configuration and data source configuration become invalid, and the created cluster is unavailable. When data sources in different domains are interconnected, HetuEngine automatically combines the **krb5.conf** file. After the domain name is changed, the domain name for Kerberos authentication changes. As a result, the information about the interconnected data source becomes invalid.

Answer
------

-  You need to reinstall the cluster client.

-  Delete the old data source information on HSConsole by referring to :ref:`Managing Data Sources <mrs_01_1720>` and configure the data source information on the HSConsole again by referring to :ref:`Configuring Data Sources <mrs_01_2314>`.
