:original_name: mrs_01_1704.html

.. _mrs_01_1704:

Blocks Miss on the NameNode UI After the Successful Rollback
============================================================

Question
--------

Why are some blocks missing on the NameNode UI after the rollback is successful?

Answer
------

This problem occurs because blocks with new IDs or genstamps may exist on the DataNode. The block files in the DataNode may have different generation flags and lengths from those in the rollback images of the NameNode. Therefore, the NameNode rejects these blocks in the DataNode and marks the files as damaged.

**Scenarios:**

#. Before an upgrade:

   Client A writes some data to file X. (Assume A bytes are written.)

2. During an upgrade:

   Client A still writes data to file X. (The data in the file is A + B bytes.)

3. After an upgrade:

   Client A completes the file writing. The final data is A + B bytes.

4. Rollback started:

   The status will be rolled back to the status before the upgrade. That is, file X in NameNode will have A bytes, but block files in DataNode will have A + B bytes.

**Recovery procedure:**

#. Obtain the list of damaged files from NameNode web UI or run the following command to obtain:

   **hdfs fsck <filepath> -list-corruptfileblocks**

#. Run the following command to delete unnecessary files:

   **hdfs fsck <corrupt file path> - delete**

   .. note::

      Deleting a file is a high-risk operation. Ensure that the files are no longer needed before performing this operation.

#. For the required files, run the **fsck** command to obtain the block list and block sequence.

   -  In the block sequence table provided, use the block ID to search for the data directory in the DataNode and download the corresponding block from the DataNode.

   -  Write all such block files in appending mode based on the sequence to construct the original file.

      Example:

      File 1--> blk_1, blk_2, blk_3

      Create a file by combining the contents of all three block files from the same sequence.

   -  Delete the old file from HDFS and rewrite the new file.
