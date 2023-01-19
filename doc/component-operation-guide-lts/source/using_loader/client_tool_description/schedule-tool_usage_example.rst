:original_name: mrs_01_1160.html

.. _mrs_01_1160:

schedule-tool Usage Example
===========================

Scenario
--------

After a job is created using the Loader WebUI or Loader-tool, use schedule-tool to execute the job.

Prerequisites
-------------

The Loader client has been installed and configured.

Procedure
---------

#. .. _mrs_01_1160__en-us_topic_0000001219149041_la615007634824ea9af1b8e5b93c0867b:

   In the directory **/opt/houjt/test03** on the SFTP server, create multiple files with **table1** as the prefix, **.txt** as the suffix, and **yyyyMMdd** as the date format in the middle of the file name.


   .. figure:: /_static/images/en-us_image_0000001295740224.png
      :alt: **Figure 1** Example

      **Figure 1** Example

#. Create a Loader job of importing data from the SFTP server to HDFS. For details, see :ref:`Typical Scenario: Importing Data from an SFTP Server to HDFS or OBS <mrs_01_1089>`.

#. Log in to the node where the client is located as the user who installs the client.

#. Run the following command to go to the **conf** directory of schedule-tool. For example, if the Loader client installation directory is **/opt/hadoopclient/Loader**, run the following command:

   **cd /opt/hadoopclient/Loader/loader-tools-1.99.3/schedule-tool/conf**

#. Run the following command to edit the schedule.properties file and configure the login mode:

   **vi schedule.properties**

   schedule-tool supports two login modes. Only one mode can be selected. For parameter details, see :ref:`schedule-tool Usage Guide <mrs_01_1159>`.

   -  When the password mode is used for login, the configuration information example is as follows:

      .. code-block::

         [server.url = 10.10.26.187:21351,127.0.0.2:21351]
         [authentication.type = kerberos]
         [use.keytab = false]
         [authentication.user = admin]
         [authentication.password= d2NjX2NyeXB0ATQxNDU1MzVGNDM0MjQzOzMwMzQzNjQ0Mzk0NTQ2NDY0MzM1MzM0NDM0NDMzMzMxNDEzMzQ1MzA0NTM0MzQ0NDQ0NDQ0NjM0MzM0MzQyNDI7OzMyMzUzMDMwOzc2NjcxMEI0M0JCRDQzQzgwQ0I4NEZGNDU3RkFDQjhBOzlCODhGNUM1RUIxQUI4QUM7NTc0MzQzNUY0MzUyNTk1MDU0NUY0NDQ1NDY0MTU1NEM1NDVGNDQ0RjRENDE0OTRFOzMwOzMxMzQzNTM2MzMzMTMyMzgzMzMzMzIzNzMwOw]

   -  When the keytab file mode is used for login, the configuration information example is as follows:

      .. code-block::

         [server.url = 10.10.26.187:21351,127.0.0.2:21351]
         [authentication.type = kerberos]
         [use.keytab = true]
         [client.principal = bar]
         [client.keytab = /opt/hadoopclient/Loader/loader-tools-1.99.3/loader-tool/hadoop-config/user.keytab]
         [krb5.conf.file = /opt/hadoopclient/Loader/loader-tools-1.99.3/loader-tool/hadoop-config/krb5.conf]

#. Run the following command to edit the job.properties file and configure job information:

   **vi job.properties**

   .. code-block::

      #job name
      job.jobName = sftp2hdfs-schedule-tool


      #Whether to update the loader configuration parameters(File filter)£?This parameter is used to match the import file name.Values are true or false.
      #false means update.the file name which is get by schedule tool will be updated to Loader configuration parameters (File filter).
      #false means no update.the file name which is get by schedule tool will be updated to Loader configuration parameters (import path).
      file.filter = false


      #File name = prefix + date + suffix
      #Need to import the file name prefix
      file.fileName.prefix=table1

      #Need to import the file name suffixes
      file.fileName.posfix=.txt

      #Date Days.Value is an integer.
      #According to the date and number of days to get the date of the import file.
      date.day = 1

      #Date Format.Import file name contains the date format.Format Type£ºyyyyMMdd,yyyyMMdd HHmmss,yyyy-MM-dd,yyyy-MM-dd HH:mm:ss
      file.date.format = yyyyMMdd

      #Date Format.Scheduling script execution. Enter the date format.
      parameter.date.format = yyyyMMdd


      #Whether the import file is a compressed format.Values ??are true or false.
      #true indicates that the file is a compressed format£?Execution scheduling tool will extract the files.false indicates that the file is an uncompressed.Execution scheduling tool does not unpack.
      file.format.iscompressed = false

      #Hadoop storage type.Values are HDFS or HBase.
      storage.type = HDFS

   According to the data provided by :ref:`1 <mrs_01_1160__en-us_topic_0000001219149041_la615007634824ea9af1b8e5b93c0867b>`, the filtering rules are set as follows when the **table120160221.txt** file is used as an example:

   -  File name prefix:

      file.fileName.prefix=table1

   -  File name suffix:

      file.fileName.posfix=.txt

   -  Date format included in the file name:

      file.date.format = yyyyMMdd

   -  Entered date parameter for invoking the script:

      parameter.date.format = yyyyMMdd

   -  Number of delayed days.

      date.day = 1

      For example, if the input date parameter of the script is **20160220**, the result is **20160221** by using the addition.

      .. note::

         If the **./run.sh 20160220 /user/loader/schedule_01** command is executed, the preceding filtering rules will be combined into a string: **"table1"+"20160221"+.txt = table120160221.txt**.

#. Select a filtering rule according to the value of **file.filter**.

   -  If a file is to be exactly matched, go to :ref:`8 <mrs_01_1160__en-us_topic_0000001219149041_lc22613a01864415a95c6937512f03fe6>`.
   -  If a series of files are to be fuzzily matched, go to :ref:`9 <mrs_01_1160__en-us_topic_0000001219149041_le84ccb022b5743d784c050fe68f30871>`.

#. .. _mrs_01_1160__en-us_topic_0000001219149041_lc22613a01864415a95c6937512f03fe6:

   Change the value of **file.filter** in the **job.properties** file to **false**.

   Run the following commands to run the job. The task is completed.

   **cd /opt/hadoopclient/Loader/loader-tools-1.99.3/schedule-tool**

   **./run.sh** *20160220* */user/loader/schedule_01*

   *20160220* indicates the input date, and */user/loader/schedule_01* indicates the output path.

   .. note::

      The string **table120160221.txt** obtained by combining the preceding filtering rules will be used as the file name and appended to the input path of the job. Therefore, the job will only process the uniquely matched file **table120160221.txt**.

#. .. _mrs_01_1160__en-us_topic_0000001219149041_le84ccb022b5743d784c050fe68f30871:

   In the **job.properties** file, change the value of **file.filter** to **true**, and set the value of **file.fileName.prefix** to **\***.

   Run the following commands to run the job. The task is completed.

   **cd /opt/hadoopclient/Loader/loader-tools-1.99.3/schedule-tool**

   **./run.sh** *20160220* */user/loader/schedule_01*

   *20160220* indicates the input date, and */user/loader/schedule_01* indicates the output path.

   .. note::

      The string **\*20160221.txt** obtained by combining the preceding filtering rules will be used as the fuzzy match mode of the file filter. In the input path of the job, all files matching **\*20160221.txt** will be processed by the job.
