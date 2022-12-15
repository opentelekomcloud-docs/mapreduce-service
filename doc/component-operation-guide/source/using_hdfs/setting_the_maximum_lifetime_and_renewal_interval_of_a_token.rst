:original_name: mrs_01_0808.html

.. _mrs_01_0808:

Setting the Maximum Lifetime and Renewal Interval of a Token
============================================================

Scenario
--------

In security mode, users can flexibly set the maximum token lifetime and token renewal interval in HDFS based on cluster requirements.

Configuration Description
-------------------------

**Navigation path for setting parameters:**

Go to the **All Configurations** page of HDFS and enter a parameter name in the search box by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.

.. table:: **Table 1** Parameter description

   +----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | Parameter                                    | Description                                                                                                                                             | Default Value |
   +==============================================+=========================================================================================================================================================+===============+
   | dfs.namenode.delegation.token.max-lifetime   | This parameter is a server parameter. It specifies the maximum lifetime of a token. Unit: milliseconds. Value range: 10,000 to 10,000,000,000,000       | 604,800,000   |
   +----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | dfs.namenode.delegation.token.renew-interval | This parameter is a server parameter. It specifies the maximum lifetime to renew a token. Unit: milliseconds. Value range: 10,000 to 10,000,000,000,000 | 86,400,000    |
   +----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
