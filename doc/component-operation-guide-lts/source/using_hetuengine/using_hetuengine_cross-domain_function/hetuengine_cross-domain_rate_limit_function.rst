:original_name: mrs_01_24284.html

.. _mrs_01_24284:

HetuEngine Cross-Domain Rate Limit Function
===========================================

#. .. _mrs_01_24284__en-us_topic_0000001219231227_li12347313587:

   Configure the **ratelimit.xml** configuration file for the HSFabric rate limit policy on the local host. The configuration template is as follows:

   .. code-block::

      <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
      <ratelimit>
          <current-domain>0755</current-domain><!-- city1 Name of zone to which the local domain data source belongs -->
          <default-bandwidth>5120</default-bandwidth><!-- The default data volume limit is 50 MB -->
          <domain-list>
              <domain>
                  <domainName>0769</domainName><!--Name of zone to which the target domain data source belongs -->
                  <bandwidth>102400</bandwidth><!-- The data volume (in KB) sent from the current domain (for exampel, city1) to the target domain (for example, city2) is 100 /MB -->
                  <cluster-list>
          <hsfabric><!-- One HSFabric Cluster -->
                          <clusterName>hsfabric01</clusterName><!-- Cluster description -->
                          <hsfabric-node>
                              <hsfabricHostPort>10.10.10.10:29900</hsfabricHostPort><!-- Host IP address of the HSFabric instance -->
                          </hsfabric-node>
                      </hsfabric>
                  </cluster-list>
              </domain>
              <domain>
                  <domainName>0770</domainName>
                  <bandwidth>20480</bandwidth><!-- The data volume (in KB) sent from the current domain (for exampel, city1) to the target domain (for example, city2) is 20 MB -->
                  <cluster-list>
                      <hsfabric><!-- One HSFabric Cluster -->
                          <clusterName>hsfabric02</clusterName>
                          <hsfabric-node>
                              <hsfabricHostPort>10.10.10.10:29900</hsfabricHostPort>
                          </hsfabric-node>
                      </hsfabric>
                  </cluster-list>
              </domain>
          </domain-list>
      </ratelimit>

   .. table:: **Table 1** Parameters in the **ratelimit.xml** file

      +-------------------+-------------------------------------------------------------------------------------------------------+-------------------+
      | Parameter         | Description                                                                                           | Example Value     |
      +===================+=======================================================================================================+===================+
      | current-domain    | Name of zone to which the local domain data source belongs                                            | 0755              |
      +-------------------+-------------------------------------------------------------------------------------------------------+-------------------+
      | default-bandwidth | Default data volume limit, in KB                                                                      | 5120              |
      +-------------------+-------------------------------------------------------------------------------------------------------+-------------------+
      | domainName        | Name of zone to which the target domain data source belongs                                           | 0769              |
      +-------------------+-------------------------------------------------------------------------------------------------------+-------------------+
      | bandwidth         | Data volume from the current zone (for example, city1) to the target zone (for example, city2), in KB | 102400            |
      +-------------------+-------------------------------------------------------------------------------------------------------+-------------------+
      | clusterName       | Description of the cluster in the target domain                                                       | hsfabric01        |
      +-------------------+-------------------------------------------------------------------------------------------------------+-------------------+
      | hsfabricHostPort  | Service IP address and port number of HSFabric in the target domain                                   | 10.10.10.10:29900 |
      +-------------------+-------------------------------------------------------------------------------------------------------+-------------------+

#. Log in to Manager where the target domain cluster locates as an administrator who can access the HetuEngine WebUI.

#. Choose **Cluster** > **Services** > **HetuEngine**. On the displayed page, click **Configurations** and then **All Configurations**.

#. Choose **HSFabric(role)** > **Rate Limit** and click **Upload File** to upload the **ratelimit.xml** file prepared in :ref:`1 <mrs_01_24284__en-us_topic_0000001219231227_li12347313587>`.

#. Click **Instance**, select the **HSFabric** instance, choose **More** > **Restart Instance**, and enter the password to restart the HSFabric instance.
