:original_name: mrs_01_1698.html

.. _mrs_01_1698:

Standby NameNode Fails to Be Restarted When the System Is Powered off During Metadata (Namespace) Storage
=========================================================================================================

Question
--------

When the standby NameNode is powered off during metadata (namespace) storage, it fails to be started and the following error information is displayed.

|image1|

Answer
------

When the standby NameNode is powered off during metadata (namespace) storage, it fails to be started and the MD5 file is damaged. Remove the damaged fsimage and start the standby NameNode to rectify the fault. After the rectification, the standby NameNode loads the previous fsimage and reproduces all edits.

Recovery procedure:

#. Run the following command to remove the damaged fsimage:

   **rm -rf ${BIGDATA_DATA_HOME}/namenode/current/fsimage_0000000000000096**

#. Start the standby NameNode.

.. |image1| image:: /_static/images/en-us_image_0000001349169981.png
