:original_name: mrs_01_1572.html

.. _mrs_01_1572:

File Systems
============

Scenario
--------

Result files are created when tasks are running. Flink enables you to configure parameters for file creation.

Configuration Description
-------------------------

Configuration items include overwriting policy and directory creation.

.. table:: **Table 1** Parameter description

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+-----------------+
   | Parameter                         | Description                                                                                                                                                                                                                        | Default Value   | Mandatory       |
   +===================================+====================================================================================================================================================================================================================================+=================+=================+
   | fs.overwrite-files                | Whether to overwrite the existing file by default when the file is written.                                                                                                                                                        | false           | No              |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+-----------------+
   | fs.output.always-create-directory | When the degree of parallelism (DOP) of file writing programs is greater than 1, a directory is created under the output file path and different result files (one for each parallel writing program) are stored in the directory. | false           | No              |
   |                                   |                                                                                                                                                                                                                                    |                 |                 |
   |                                   | -  If this parameter is set to **true**, a directory is created for the writing program whose DOP is 1 and a result file is stored in the directory.                                                                               |                 |                 |
   |                                   | -  If this parameter is set to **false**, the file of the writing program whose DOP is 1 is created directly in the output path and no directory is created.                                                                       |                 |                 |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+-----------------+
