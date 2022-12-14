:original_name: mrs_01_24479.html

.. _mrs_01_24479:

Common Oozie Troubleshooting Methods
====================================

#. Check the job logs on Yarn. Run the command executed through Hive SQL using beeline to ensure that Hive is running properly.
#. If error information such as "classnotfoundException" is displayed, check whether the JAR package of the faulty class exists in the **/user/oozie/share/lib** directory of each component. If no, add the JAR package and go to :ref:`Why Update of the share lib Directory of Oozie on HDFS Does Not Take Effect? <mrs_01_1847>`. If the faulty class still cannot be found after the **share lib** directory is updated, check whether **sharelibDirNew** is **/user/oozie/share/lib** in the output of the command for updating the directory.\ |image1|
#. If "NosuchMethodError" is displayed, check whether the JAR packages of each component in the **/user/oozie/share/lib** directory have multiple versions. Note that the JAR packages uploaded by the service cannot conflict with each other. You can check whether a JAR package conflict occurs based on the loaded JAR packages in Oozie run logs on Yarn.
#. If the self-developed code is abnormal, run the Oozie sample to check whether Oozie is running properly.
#. Contact technical support personnel. By using this method, you must collect run logs of Oozie on Yarn, Oozie logs, and component run logs. For example, if an exception occurs when Hive runs on Oozie, you need to collect Hive logs.

.. |image1| image:: /_static/images/en-us_image_0000001349289617.png
