:original_name: mrs_01_1769.html

.. _mrs_01_1769:

How Do I Solve the Problem that Kafka Topics Cannot Be Deleted?
===============================================================

Question
--------

How do I delete a Kafka topic if it fails to be deleted?

Answer
------

-  Possible cause 1: The **delete.topic.enable** configuration item is not set to **true**. The deletion can be performed only when the configuration item is set to **true**.
-  Possible cause 2: The **auto.create.topics.enable** configuration parameter is set to **true**, which is used by other applications and is always running in the background.

Solution:

-  For cause 1: Set **delete.topic.enable** to **true** on the configuration page.
-  For cause 2: Stop the application that uses the topic in the background, or set **auto.create.topics.enable** to **false** (restart the Kafka service), and then delete the topic.
