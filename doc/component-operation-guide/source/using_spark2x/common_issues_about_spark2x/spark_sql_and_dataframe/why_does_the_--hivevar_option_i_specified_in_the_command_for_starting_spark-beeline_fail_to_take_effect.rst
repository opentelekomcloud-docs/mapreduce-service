:original_name: mrs_01_2040.html

.. _mrs_01_2040:

Why Does the "--hivevar" Option I Specified in the Command for Starting spark-beeline Fail to Take Effect?
==========================================================================================================

Question
--------

Why does the **--hivevar** option I specified in the command for starting spark-beeline fail to take effect?

In the V100R002C60 version, if I use the **--hivevar <VAR_NAME>=<var_value>** option to define a variable in the command for starting spark-beeline, no error is reported in spark-beeline. However, if the variable *<VAR_NAME>* is used in SQL, the variable cannot be parsed and the <VAR_NAME> exception is reported.

For example:

#. Run the following command to start the spark-beeline:

   **spark-beeline --hivevar <VAR_NAME>=<var_value>**

2. After spark-beeline is started successfully, I run the SQL statements **DROP TABLE ${VAR_NAME}** in spark-beeline. The VAR_NAME exception occurs.

Answer
------

In the V100R002C60 version, the **--hivevar <VAR_NAME>=<var_value>** feature of Hive is not supported in Spark because multi-session management function is added. Therefore, the **--hivevar** option in the command for starting spark-beeline is invalid.
