:original_name: mrs_03_1194.html

.. _mrs_03_1194:

**beeline -e**\ How Do I Do If an Error Occurs When Hive Runs the beeline -e Command to Execute Multiple Statements?
====================================================================================================================

When Hive of MRS 3.\ *x* runs the **beeline -e " use default;show tables;"** command, the following error message is displayed: Error while compiling statement: FAILED: ParseException line 1:11 missing EOF at ';' near 'default' (state=42000,code=40000).

Solutions:

-  Method 1: Replace the **beeline -e " use default;show tables;"** command with **beeline --entirelineascommand=false -e "use default;show tables;"**.
-  Method 2:

   #. In the **/opt/Bigdata/client/Hive** directory on the Hive client, change **export CLIENT_HIVE_ENTIRELINEASCOMMAND=true** in the **component_env** file to **export CLIENT_HIVE_ENTIRELINEASCOMMAND=false**.


      .. figure:: /_static/images/en-us_image_0000001392414806.png
         :alt: **Figure 1** Changing the **component_env** file

         **Figure 1** Changing the **component_env** file

   #. Run the following command to verify the configuration:

      **source /opt/Bigdata/client/bigdata_env**

      **beeline -e " use default;show tables;"**
