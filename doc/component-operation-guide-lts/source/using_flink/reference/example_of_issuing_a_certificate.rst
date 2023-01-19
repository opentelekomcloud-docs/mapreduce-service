:original_name: mrs_01_0621.html

.. _mrs_01_0621:

Example of Issuing a Certificate
================================

Generate the **generate_keystore.sh** script based on the sample code and save the script to the **bin** directory on the Flink client.

.. code-block::

   #!/bin/bash

   KEYTOOL = ${JAVA_HOME}/bin/keytool
   KEYSTOREPATH = "$FLINK_HOME/conf/"
   CA_ALIAS = "ca"
   CA_KEYSTORE_NAME = "ca.keystore"
   CA_DNAME = "CN=Flink_CA"
   CA_KEYALG = "RSA"
   CLIENT_CONF_YAML = "$FLINK_HOME/conf/flink-conf.yaml"
   KEYTABPRINCEPAL = ""

   function getConf() {
       if [$# - ne 2];
       then
       echo "invalid parmaters for getConf"
       exit 1
       fi

       confName = "$1"
       if [-z "$confName"];
       then
       echo "conf name is empty."
       exit 2
       fi

       configFile = $FLINK_HOME / conf / client.properties
       if [!-f $configFile];
       then
       echo $configFile " is not exist."
       exit 3
       fi

       defaultValue = "$2"
       cnt = $(grep $1 $configFile | wc - l)
       if [$cnt - gt 1];
       then
       echo $confName " has multi values in "
       $configFile
       exit 4
       elif[$cnt - lt 1];
       then
       echo $defaultValue
       else
           line = $(grep $1 $configFile)
       confValue = $(echo "${line#*=}")
       echo "$confValue"
       fi
   }

   function createSelfSignedCA() {#
       varible from user input
       keystorePath = $1
       storepassValue = $2
       keypassValue = $3

       # generate ca keystore
       rm - rf $keystorePath / $CA_KEYSTORE_NAME
       $KEYTOOL - genkeypair - alias $CA_ALIAS - keystore $keystorePath / $CA_KEYSTORE_NAME - dname $CA_DNAME - storepass $storepassValue - keypass $keypassValue - validity 3650 - keyalg $CA_KEYALG - keysize 3072 - ext bc = ca: true
       if [$ ? -ne 0];
       then
       echo "generate ca.keystore failed."
       exit 1
       fi

       # generate ca.cer
       rm - rf "$keystorePath/ca.cer"
       $KEYTOOL - keystore "$keystorePath/$CA_KEYSTORE_NAME" - storepass "$storepassValue" - alias $CA_ALIAS - validity 3650 - exportcert > "$keystorePath/ca.cer"
       if [$ ? -ne 0];
       then
       echo "generate ca.cer failed."
       exit 1
       fi

       # generate ca.truststore
       rm - rf "$keystorePath/flink.truststore"
       $KEYTOOL - importcert - keystore "$keystorePath/flink.truststore" - alias $CA_ALIAS - storepass "$storepassValue" - noprompt - file "$keystorePath/ca.cer"
       if [$ ? -ne 0];
       then
       echo "generate ca.truststore failed."
       exit 1
       fi
   }

   function generateKeystore() {#
       get path / pass from input
       keystorePath = $1
       storepassValue = $2
       keypassValue = $3

       # get value from conf
       aliasValue = $(getConf "flink.keystore.rsa.alias"
           "flink")
       validityValue = $(getConf "flink.keystore.rsa.validity"
           "3650")
       keyalgValue = $(getConf "flink.keystore.rsa.keyalg"
           "RSA")
       dnameValue = $(getConf "flink.keystore.rsa.dname"
           "CN=flink.com")
       SANValue = $(getConf "flink.keystore.rsa.ext"
           "ip:127.0.0.1")
       SANValue = $(echo "$SANValue" | xargs)
       SANValue = "ip:$(echo "
       $SANValue "| sed 's/,/,ip:/g')"

       #
       generate keystore
       rm - rf $keystorePath / flink.keystore
       $KEYTOOL - genkeypair - alias $aliasValue - keystore $keystorePath / flink.keystore - dname $dnameValue - ext SAN = $SANValue - storepass $storepassValue - keypass $keypassValue - keyalg $keyalgValue - keysize 3072 - validity 3650
       if [$ ? -ne 0];then
       echo "generate flink.keystore failed."
       exit 1
       fi

       # generate cer
       rm - rf $keystorePath / flink.csr
       $KEYTOOL - certreq - keystore $keystorePath / flink.keystore - storepass $storepassValue - alias $aliasValue - file $keystorePath / flink.csr
       if [$ ? -ne 0];then
       echo "generate flink.csr failed."
       exit 1
       fi

       # generate flink.cer
       rm - rf $keystorePath / flink.cer
       $KEYTOOL - gencert - keystore $keystorePath / ca.keystore - storepass $storepassValue - alias $CA_ALIAS - ext SAN = $SANValue - infile $keystorePath / flink.csr - outfile $keystorePath / flink.cer - validity 3650
       if [$ ? -ne 0];then
       echo "generate flink.cer failed."
       exit 1
       fi

       #
       import cer into keystore
       $KEYTOOL - importcert - keystore $keystorePath / flink.keystore - storepass $storepassValue - file $keystorePath / ca.cer - alias $CA_ALIAS - noprompt
       if [$ ? -ne 0];then
       echo "importcert ca."
       exit 1
       fi

       $KEYTOOL - importcert - keystore $keystorePath / flink.keystore - storepass $storepassValue - file $keystorePath / flink.cer - alias $aliasValue - noprompt;
       if [$ ? -ne 0];then
       echo "generate flink.truststore failed."
       exit 1
       fi
   }

   function configureFlinkConf() {#
       set config
       if [-f "$CLIENT_CONF_YAML"];then
       SSL_ENCRYPT_ENABLED = $(grep "security.ssl.encrypt.enabled"
           "$CLIENT_CONF_YAML" | awk '{print $2}')
       if ["$SSL_ENCRYPT_ENABLED" = "false"];then

       sed - i s / "security.ssl.key-password:".*/"security.ssl.key-password:"\ "${keyPass}"/g
       "$CLIENT_CONF_YAML"
       if [$ ? -ne 0];then
       echo "set security.ssl.key-password failed."
       return 1
       fi

       sed - i s / "security.ssl.keystore-password:".*/"security.ssl.keystore-password:"\ "${storePass}"/g
       "$CLIENT_CONF_YAML"
       if [$ ? -ne 0];then
       echo "set security.ssl.keystore-password failed."
       return 1
       fi

       sed - i s / "security.ssl.truststore-password:".*/"security.ssl.truststore-password:"\ "${storePass}"/g
       "$CLIENT_CONF_YAML"
       if [$ ? -ne 0];then
       echo "set security.ssl.keystore-password failed."
       return 1
       fi

       echo "security.ssl.encrypt.enabled is false, set security.ssl.key-password security.ssl.keystore-password security.ssl.truststore-password success."
       else
           echo "security.ssl.encrypt.enabled is true, please enter security.ssl.key-password security.ssl.keystore-password security.ssl.truststore-password encrypted value in flink-conf.yaml."
       fi

       keystoreFilePath = "${keystorePath}" / flink.keystore
       sed - i 's#'
       "security.ssl.keystore:".*'#'
       "security.ssl.keystore:"\
       "$keystoreFilePath"
       '#g'
       "$CLIENT_CONF_YAML"
       if [$ ? -ne 0];then
       echo "set security.ssl.keystore failed."
       return 1
       fi


       truststoreFilePath = "${keystorePath}/flink.truststore"
       sed - i 's#'
       "security.ssl.truststore:".*'#'
       "security.ssl.truststore:"\
       "$truststoreFilePath"
       '#g'
       "$CLIENT_CONF_YAML"
       if [$ ? -ne 0];then
       echo "set security.ssl.truststore failed."
       return 1
       fi

       command - v sha256sum > /dev/null
       if [$ ? -ne 0];then
       echo "sha256sum is not exist, it will produce security.cookie with date +%F-%H-%M-%s-%N."
       cookie = $(date + % F - % H - % M - % s - % N)
       else
           cookie = "$(echo "
       $ {
           KEYTABPRINCEPAL
       }
       "| sha256sum | awk '{print $1}')"
       fi

       sed - i s / "security.cookie:".*/"security.cookie:"\ "${cookie}"/g
       "$CLIENT_CONF_YAML"
       if [$ ? -ne 0];then
       echo "set security.cookie failed."
       return 1
       fi
       fi
       return 0;
   }

   main() {
       #check environment variable is set or not
       if [-z $ {
           FLINK_HOME + x
       }];
       then
       echo "errro: environment variables are not set."
       exit 1
       fi
       stty -echo
       read -rp "Enter password:"
       password
       stty echo
       echo

       KEYTABPRINCEPAL = $(grep "security.kerberos.login.principal"
           "$CLIENT_CONF_YAML" | awk '{print $2}')
       if [-z "$KEYTABPRINCEPAL"];
       then
       echo "please config security.kerberos.login.principal info first."
       exit 1
       fi


       # get input
       keystorePath = "$KEYSTOREPATH"
       storePass = "$password"
       keyPass = "$password"

       #
       generate self signed CA
       createSelfSignedCA "$keystorePath"
       "$storePass"
       "$keyPass"
       if [$ ? -ne 0];
       then
       echo "create self signed ca failed."
       exit 1
       fi

       # generate keystore
       generateKeystore "$keystorePath"
       "$storePass"
       "$keyPass"
       if [$ ? -ne 0];
       then
       echo "create keystore failed."
       exit 1
       fi

       echo "generate keystore/truststore success."

       #
       set flink config
       configureFlinkConf "$keystorePath"
       "$storePass"
       "$keyPass"
       if [$ ? -ne 0];
       then
       echo "configure Flink failed."
       exit 1
       fi

       return 0;
   }

   #
   the start main
   main "$@"

   exit 0

.. note::

   Run the **sh generate_keystore.sh** *<password>* command. *<password>* is user-defined.

   -  If *<password>* contains the special character **$**, use the following method to avoid the password being escaped: **sh generate_keystore.sh 'Bigdata_2013'**.
   -  The password cannot contain **#**.
   -  Before using the **generate_keystore.sh** script, run the **source bigdata_env** command in the client directory.
   -  When the **generate_keystore.sh** script is used, the absolute paths of **security.ssl.keystore** and **security.ssl.truststore** are automatically filled in **flink-conf.yaml**. Therefore, you need to manually change the paths to relative paths as required. Example:

      -  Change **/opt/client/Flink/flink/conf//flink.keystore** to **security.ssl.keystore: ssl/flink.keystore**.
      -  Change **/opt/client/Flink/flink/conf//flink.truststore** to **security.ssl.truststore: ssl/flink.truststore**.
      -  Create the **ssl** folder in any directory on the Flink client. For example, create the **ssl** folder in the **/opt/client/Flink/flink/conf/** directory and save the **flink.keystore** and **flink.truststore** files to the **ssl** folder.
      -  When running the **yarn-session** or **flink run -m yarn-cluster** command, run the **yarn-session -t ssl -d** or **flink run -m yarn-cluster -yt ssl -d WordCount.jar** command in the same directory as the **ssl** folder.
