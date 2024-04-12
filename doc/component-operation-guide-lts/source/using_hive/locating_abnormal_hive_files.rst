:original_name: mrs_01_24480.html

.. _mrs_01_24480:

Locating Abnormal Hive Files
============================

Scenario
--------

-  Data files stored in Hive are abnormal due to misoperations or disk damage, thereby causing task execution failures or incorrect data results.
-  Common non-text data files can be located using the specified tool.

   .. note::

      This section applies only to MRS 3.2.0 or later.

Procedure
---------

#. Log in to the node where the Hive service is installed as user **omm** and run the following command to go to the Hive installation directory:

   **cd ${BIGDATA_HOME}/FusionInsight_HD_*/install/FusionInsight-Hive-*/hive-*/bin**

#. Run the following tool to locate abnormal Hive files:

   **sh hive_parser_file.sh [--help] <filetype> <command> <input-file|input-directory>**

   :ref:`Table 1 <mrs_01_24480__table11352804551>` describes the related parameters.

   Note: You can run only one command at a time.

   .. _mrs_01_24480__table11352804551:

   .. table:: **Table 1** Parameter description

      +-----------------+------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter       | Description                                                                                                                  | Remarks                                                                                                                                                                                        |
      +=================+==============================================================================================================================+================================================================================================================================================================================================+
      | filetype        | Specifies the format of the data file to be parsed. Currently, only the ORC, RC (RCFile), and Parquet formats are supported. | Currently, data files in the RC format can only be viewed.                                                                                                                                     |
      +-----------------+------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -c              | Prints the column information in the current metadata.                                                                       | The column information includes the class name, file format, and sequence number.                                                                                                              |
      +-----------------+------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -d              | Prints data in a data file. You can limit the data volume using the **limit** parameter.                                     | The data is the content of the specified data file. Note that only one value can be specified for the **limit** parameter at a time.                                                           |
      +-----------------+------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -t              | Prints the time zone to which the data is written.                                                                           | The time zone is the zone to which the file is written.                                                                                                                                        |
      +-----------------+------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -h              | Prints the help information.                                                                                                 | Help information.                                                                                                                                                                              |
      +-----------------+------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -m              | Prints information about various storage formats.                                                                            | The information varies based on the storage format. For example, if the file format is ORC, information such as strip and block size will be printed.                                          |
      +-----------------+------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | -a              | Prints detailed information.                                                                                                 | The detailed information, including the preceding parameters, is displayed.                                                                                                                    |
      +-----------------+------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | input-file      | Specifies the data files to be input.                                                                                        | If the input directory contains a file of the supported formats, the file will be parsed. Otherwise, this operation is omitted. You can specify a local file or an HDFS/OBS file or directory. |
      +-----------------+------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | input-directory | Specifies the directory where the input data file is located. This parameter is used when there are multiple subfiles.       |                                                                                                                                                                                                |
      +-----------------+------------------------------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Example:

   **sh hive_parser_file.sh orc -d limit=100 hdfs://hacluster/user/hive/warehouse/orc_test**

   If the file name does not contain a prefix similar to **hdfs://hacluster**, the local file is read by default.
