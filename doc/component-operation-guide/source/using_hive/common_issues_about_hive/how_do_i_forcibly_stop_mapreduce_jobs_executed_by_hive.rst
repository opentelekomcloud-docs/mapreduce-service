:original_name: mrs_01_1756.html

.. _mrs_01_1756:

How Do I Forcibly Stop MapReduce Jobs Executed by Hive?
=======================================================

Question
--------

How do I stop a MapReduce task manually if the task is suspended for a long time?

Answer
------

#. Log in to FusionInsight Manager.
#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Yarn**.
#. On the left pane, click **ResourceManager(Host name, Active)**, and log in to Yarn.
#. Click the button corresponding to the task ID. On the task page that is displayed, click **Kill Application** in the upper left corner and click **OK** in the displayed dialog box to stop the task.
