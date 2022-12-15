:original_name: mrs_01_0449.html

.. _mrs_01_0449:

Kafka Data
==========

MirrorMaker is a powerful tool for Kafka data synchronization. It is used when data needs to be synchronized between two Kafka clusters or when data in the original Kafka cluster needs to be migrated to a new Kafka cluster. MirrorMaker is a built-in tool in Kafka. It actually integrates the functions of Kafka Consumer and Producer. MirrorMaker can read data from one Kafka cluster and write the data to another Kafka cluster to implement data synchronization between Kafka clusters.

This section describes how to use the MirrorMaker tool provided by MRS to synchronize and migrate Kafka cluster data. Before migrating Kafka data, ensure that the two clusters can communicate with each other by following the instructions provided in :ref:`Establishing a Data Transmission Channel <mrs_01_0445__section2349182854814>`.

Procedure
---------

**Versions earlier than MRS 3.x:**

#. .. _mrs_01_0449__li1980875616292:

   Enable the Kerberos authentication for clusters.

#. If you plan to use the MirrorMaker tool in a source cluster, log in to MRS Manager of a destination cluster and choose **Services**. If you plan to use the MirrorMaker tool in a destination cluster, log in to MRS Manager of a source cluster and choose **Services**.

#. Choose **Kafka** > **Service Configuration**, and change **Basic** to **All** in the parameter type drop-down box.

#. Click **Broker** > **Customization** and add the following rules on the displayed page:

   **sasl.kerberos.principal.to.local.rules = RULE:[1:$1@$0](.*@XXXYYYZZZ.COM)s/@.*//,RULE:[2:$1@$0](.*@ XXXYYYZZZ.COM)s/@.*//,DEFAULT**

   In the preceding rule, **XXXYYYZZZ.COM** indicates the domain name of the cluster (source cluster) where data resides. The domain name must be spelled in uppercase letters.

#. .. _mrs_01_0449__li854919509282:

   Click **Save Configuration** and select **Restart the affected services or instances**. Click **Yes** to restart the Kafka service.

   .. note::

      For a security cluster with the Kerberos authentication enabled, perform :ref:`1 <mrs_01_0449__li1980875616292>` to :ref:`5 <mrs_01_0449__li854919509282>`. For a normal cluster with the Kerberos authentication disabled, skip :ref:`1 <mrs_01_0449__li1980875616292>` to :ref:`5 <mrs_01_0449__li854919509282>` and go to :ref:`6 <mrs_01_0449__li3402143084520>`.

#. .. _mrs_01_0449__li3402143084520:

   In the cluster that uses the MirrorMaker tool, go to the cluster details page and choose **Services**.

#. Choose **Kafka** > **Service Configuration**, change **Basic** to **All** in the parameter type drop-down box, and change **All Roles** to **MirrorMaker**.

   Parameter description:

   -  The **bootstrap.servers** parameter in the **source** and **dest** tags indicates the **broker** node list and port information of the source and destination Kafka clusters respectively.
   -  Set parameter **security.protocol** in the **source** and **dest** tags based on the actual configurations of the source and destination Kafka clusters.
   -  If the source Kafka cluster or destination Kafka cluster is a security cluster, you need to set **kerberos.domain.name** and **sasl.kerberos.service.name** in the **source** and **dest** tags. If the local host is used, you do not need to set **kerberos.domain.name**. If the local host is not used, set **kerberos.domain.name** and **sasl.kerberos.service.name** based on the site requirements. The default value of **sasl.kerberos.service.name** is **kafka**.
   -  Set **whitelist** in the **mirror** tag, that is, the name of the topic to be synchronized.

#. Click **Save Configuration** and select **Restart the affected services or instances**. Click **Yes** to restart the MirrorMaker instance.

   After MirrorMaker is restarted, the data migration task is started.
