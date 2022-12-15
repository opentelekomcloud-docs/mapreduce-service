:original_name: mrs_03_1119.html

.. _mrs_03_1119:

Where Can I View Hive Metadata?
===============================

-  If Hive metadata is stored in GaussDB of an MRS cluster, log in to the master DBServer node of the cluster, switch to user **omm**, and run the **gsql -p 20051 -U {USER} -W {PASSWD} -d hivemeta** command to view the metadata.
-  If Hive metadata is stored in an external relational database, perform the following steps:

   #. On the cluster **Dashboard** page, click **Manage** on the right of **Data Connection**.

   #. .. _mrs_03_1119__li1120232084010:

      On the displayed page, obtain the value of **Data Connection ID**.

   #. On the MRS console, click **Data Connections**.

   #. In the data connection list, locate the data connection based on the data connection ID obtained in :ref:`2 <mrs_03_1119__li1120232084010>`.

   #. Click **Edit** in the **Operation** column of the data connection.

      The **RDS Instance** and **Database** indicate the relational database in which the Hive metadata is stored.
