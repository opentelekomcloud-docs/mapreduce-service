:original_name: mrs_01_2052.html

.. _mrs_01_2052:

Why Does the Spark Streaming Application Fail to Be Submitted After the Token Validity Period Expires?
======================================================================================================

Question
--------

Change the validity period of the Kerberos ticket and HDFS token to 5 minutes, set **dfs.namenode.delegation.token.renew-interval** to a value less than 60 seconds, and submit the Spark Streaming application. If the token expires, the error message below is displayed, and the application exits. Why?

.. code-block::

   token (HDFS_DELEGATION_TOKEN token 17410 for spark2x) is expired

Answer
------

-  Possible causes:

   The credential refresh thread of the ApplicationMaster process uploads the updated credential file to the HDFS based on the\ * token renew period multiplied by 0.75*.

   In the executor process, the credential refresh thread obtains the updated credential file from the HDFS based on the time ratio of the *token renewal period multiplied by 0.8* to update the token in UserGroupInformation, preventing the token from being invalid.

   When the credential refresh thread of the executor process detects that the current time is later than the credential file update time (*token renew period x 0.8*), it waits for 1 minute and then obtains the latest credential file from the HDFS to ensure that the AM has stored the updated credential file in the HDFS.

   When the value of **dfs.namenode.delegation.token.renew-interval** is less than 60 seconds, the started executor detects that the current time is later than the time when the credential file is updated. One minute later, the executor obtains the latest credential file from the HDFS. However, the token is already invalid, and the task fails to be executed. Then, other executor processes retry within 1 minute. The task also fails to run on other executors. As a result, the executors that fail to run are added to the blacklist. If no executors are available, the application exits.

-  Solution:

   In the Spark application scenario, set **dfs.namenode.delegation.token.renew-interval** to a value greater than 80 seconds. For details about the **dfs.namenode.delegation.token.renew-interval** parameter, see :ref:`Table 1 <mrs_01_2052__tccf0b141ec0540cb9da0cde471a287aa>`.

   .. _mrs_01_2052__tccf0b141ec0540cb9da0cde471a287aa:

   .. table:: **Table 1** Parameter description

      +----------------------------------------------+---------------------------------------------------------------------------------------------------------------+---------------+
      | Parameter                                    | Description                                                                                                   | Default Value |
      +==============================================+===============================================================================================================+===============+
      | dfs.namenode.delegation.token.renew-interval | This parameter is a server parameter. It specifies the maximum lifetime to renew a token. Unit: milliseconds. | 86400000      |
      +----------------------------------------------+---------------------------------------------------------------------------------------------------------------+---------------+
