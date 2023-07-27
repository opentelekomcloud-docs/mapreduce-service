:original_name: mrs_03_1212.html

.. _mrs_03_1212:

How Do I Do If Trust Relationships Between Nodes Are Abnormal?
==============================================================

If "ALM-12066 Inter-Node Mutual Trust Fails" is reported on Manager or there is no SSH trust relationship between nodes, rectify the fault by performing the following operations:

#. Run the **ssh-add -l** command on both nodes of the trusted cluster to check whether there are identities.

   |image1|

#. If no identities are displayed, run the **ps -ef|grep ssh-agent** command to find the ssh-agent process, kill the process, and wait for the process to automatically restart.

   |image2|

#. Run the **ssh-add -l** command to check whether the identities have been added. If yes, manually run the **ssh** command to check whether the trust relationship is normal.

   |image3|

#. If identities exist, check whether the **authorized_keys** file in the **/home/omm/.ssh** directory contains the information in the **id_rsa.pub** file in the **/home/omm/.ssh** of the peer node. If no, manually add the information about the peer node.

#. Check whether the permissions on the files in **/home/omm/.ssh** directory are correct.

#. Check the **/var/log/Bigdata/nodeagent/scriptlog/ssh-agent-monitor.log** file.

#. If the **home** directory of user **omm** is deleted, contact MRS support personnel.

.. |image1| image:: /_static/images/en-us_image_0000001392255270.png
.. |image2| image:: /_static/images/en-us_image_0000001392414786.png
.. |image3| image:: /_static/images/en-us_image_0000001442654033.png
