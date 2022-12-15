:original_name: mrs_01_1657.html

.. _mrs_01_1657:

Insufficient Rights When a Tenant Accesses Phoenix
==================================================

Question
--------

When a tenant accesses Phoenix, a message is displayed indicating that the tenant has insufficient rights.

Answer
------

You need to associate the HBase service and Yarn queues when creating a tenant.

The tenant must be granted additional rights to perform operations on Phoenix, that is, the RWX permission on the Phoenix system table.

Example:

Tenant **hbase** has been created. Log in to the HBase Shell as user **admin** and run the **scan 'hbase:acl'** command to query the role of the tenant. The role is **hbase_1450761169920** (in the format of tenant name_timestamp).

Run the following commands to grant rights to the tenant (if the Phoenix system table has not been generated, log in to the Phoenix client as user **admin** first and then grant rights on the HBase Shell):

**grant '@hbase_1450761169920','RWX','SYSTEM.CATALOG'**

**grant '@hbase_1450761169920','RWX','SYSTEM.FUNCTION'**

**grant '@hbase_1450761169920','RWX','SYSTEM.SEQUENCE'**

**grant '@hbase_1450761169920','RWX','SYSTEM.STATS'**

Create user **phoenix** and bind it with tenant **hbase**, so that tenant **hbase** can access the Phoenix client as user **phoenix**.
