:original_name: mrs_01_1709.html

.. _mrs_01_1709:

NameNode Fails to Be Restarted Due to EditLog Discontinuity
===========================================================

Question
--------

If a JournalNode server is powered off, the data directory disk is fully occupied, and the network is abnormal, the EditLog sequence number on the JournalNode is inconsecutive. In this case, the NameNode restart may fail.

Symptom
-------

The NameNode fails to be restarted. The following error information is reported in the NameNode run logs:

|image1|

Solution
--------

#. Find the active NameNode before the restart, go to its data directory (you can obtain the directory, such as **/srv/BigData/namenode/current** by checking the configuration item **dfs.namenode.name.dir**), and obtain the sequence number of the latest FsImage file, as shown in the following figure:

   |image2|

#. Check the data directory of each JournalNode (you can obtain the directory such as\ **/srv/BigData/journalnode/hacluster/current** by checking the value of the configuration item **dfs.journalnode.edits.dir**), and check whether the sequence number starting from that obtained in step 1 is consecutive in edits files. That is, you need to check whether the last sequence number of the previous edits file is consecutive with the first sequence number of the next edits file. (As shown in the following figure, edits_0000000000013259231-0000000000013259237 and edits_0000000000013259239-0000000000013259246 are not consecutive.)

   |image3|

#. If the edits files are not consecutive, check whether the edits files with the related sequence number exist in the data directories of other JournalNodes or NameNode. If the edits files can be found, copy a consecutive segment to the JournalNode.

#. In this way, all inconsecutive edits files are restored.

#. Restart the NameNode and check whether the restart is successful. If the fault persists, contact technical support.

.. |image1| image:: /_static/images/en-us_image_0000001349289573.png
.. |image2| image:: /_static/images/en-us_image_0000001348770293.png
.. |image3| image:: /_static/images/en-us_image_0000001295930432.png
