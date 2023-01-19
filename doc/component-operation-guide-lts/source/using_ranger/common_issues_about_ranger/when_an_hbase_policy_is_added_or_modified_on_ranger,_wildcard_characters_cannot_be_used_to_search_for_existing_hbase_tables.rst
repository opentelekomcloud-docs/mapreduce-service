:original_name: mrs_01_2355.html

.. _mrs_01_2355:

When an HBase Policy Is Added or Modified on Ranger, Wildcard Characters Cannot Be Used to Search for Existing HBase Tables
===========================================================================================================================

Question
--------

When a Ranger access permission policy is added for HBase and wildcard characters are used to search for an existing HBase table in the policy, the table cannot be found. The following error is reported in **/var/log/Bigdata/ranger/rangeradmin/ranger-admin-*log**:

.. code-block::

   Caused by: javax.security.sasl.SaslException: No common protection layer between client and server
   at com.sun.security.sasl.gsskerb.GssKrb5Client.doFinalHandshake(GssKrb5Client.java:253)
   at com.sun.security.sasl.gsskerb.GssKrb5Client.evaluateChallenge(GssKrb5Client.java:186)
   at org.apache.hadoop.hbase.security.AbstractHBaseSaslRpcClient.evaluateChallenge(AbstractHBaseSaslRpcClient.java:142)
   at org.apache.hadoop.hbase.security.NettyHBaseSaslRpcClientHandler$2.run(NettyHBaseSaslRpcClientHandler.java:142)
   at org.apache.hadoop.hbase.security.NettyHBaseSaslRpcClientHandler$2.run(NettyHBaseSaslRpcClientHandler.java:138)
   at java.security.AccessController.doPrivileged(Native Method)
   at javax.security.auth.Subject.doAs(Subject.java:422)
   at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1761)
   at org.apache.hadoop.hbase.security.NettyHBaseSaslRpcClientHandler.channelRead0(NettyHBaseSaslRpcClientHandler.java:138)
   at org.apache.hadoop.hbase.security.NettyHBaseSaslRpcClientHandler.channelRead0(NettyHBaseSaslRpcClientHandler.java:42)
   at org.apache.hbase.thirdparty.io.netty.channel.SimpleChannelInboundHandler.channelRead(SimpleChannelInboundHandler.java:105)
   at org.apache.hbase.thirdparty.io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:362)

Answer
------

The value of **hbase.rpc.protection** of the HBase service plug-in on Ranger must be the same as that of **hbase.rpc.protection** on the HBase server.

#. Log in to the Ranger management page. For details, see :ref:`Logging In to the Ranger Web UI <mrs_01_1850>`.
#. In the **HBASE** area on the home page, click the component plug-in name, for example, the |image1| button of HBase.
#. Search for the configuration item **hbase.rpc.protection** and change its value to the value of **hbase.rpc.protection** on the HBase server.
#. Click **Save**.

.. |image1| image:: /_static/images/en-us_image_0000001296219652.png
