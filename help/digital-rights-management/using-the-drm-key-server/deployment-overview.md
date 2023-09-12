---
title: Deploying the Primetime DRM Key Server overview
description: Deploying the Primetime DRM Key Server overview
copied-description: yes
exl-id: d70e8315-ed35-4159-842b-5066a2b1c4f0
---
# Deploy the Primetime DRM Key Server {#deploy-the-primetime-drm-key-server}

Before deploying the Primetime DRM Key Server, make sure that you have installed the required versions of Java and Tomcat. See, [DRM Key Server Requirements](../../digital-rights-management/using-the-drm-key-server/requirements.md).

The Primetime DRM Key Server download includes [!DNL faxsks.war]. To deploy this WAR file, copy the file to Tomcat's [!DNL webapps] directory. If you have previously deployed the WAR file, you may need to manually delete the unpacked WAR directory, [!DNL faxsks] in Tomcat's [!DNL webapps] directory). To prevent Tomcat from unpacking WAR files, edit the [!DNL server.xml] file in Tomcat's [!DNL conf] directory and set the `unpackWARs` attribute to `false`.

The Primetime DRM Key Server optionally uses a platform-specific library (`jsafe.dll` on Windows or `libjsafe.so` on Linux) for improved performance. Copy the appropriate library for your platform from `thirdparty/cryptoj/platform` to a location specified by the `PATH` environment variable (or `LD_LIBRARY_PATH` on Linux).

>[!NOTE]
>
>The 64-bit version of the [!DNL jsafe] library should only be used if both the operating system and JDK support 64-bit, otherwise use the 32-bit version.

## SSL configuration {#ssl-configuration}

SSL is required for Remote HTTPS key delivery. The SSL connections could be handled by the application server (i.e., by configuring SSL in Tomcat) or could be handled at another server (i.e., a Load balancer, SSL accelerator, or Apache). Remote HTTPS key delivery requires an SSL connection. The server needs an SSL certificate issued by a trusted CA.

There are a variety of options for configuring SSL. Below are examples for configuring SSL with client authentication in Apache and Tomcat.

The following example shows the Apache SSL configuration: 

```
SSLEngineon 
SSLCertificateFile "certs/server_cert.pem" 
SSLCertificateKeyFile "certs/server_key.pem" 
SSLOptions +StdEnvVars +FakeBasicAuth -ExportCertData +StrictRequire 
SSLRequireSSL 
ProxyRequests Off 
ProxyPass /https://keyserver-name:port/ 
ProxyPassReverse /https://keyserver-name:port/
```

The following example shows the Tomcat SSL configuration. To generate certificate and key files: 

```
Generate key:  
 openssl genrsa -des3 -out server.key 1024 
Generate CSR: 
 openssl req -new -key server.key -out server.csr 
Generate Certificate: 
 openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.cer
```

When prompted for the common name, use your server's Fully Qualified Domain Name (FQDN).

Copy [!DNL server.cer], and [!DNL server.key] to the Tomcat directory. Specify the following Connector in [!DNL conf/server.xml]: 

```
<Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true" 
 maxThreads="150" scheme="https" secure="true" 
 sslProtocol="TLS" 
 SSLCertificateFile="${catalina.base}/server.cer" 
 SSLCertificateKeyFile="${catalina.base}/server.key" 
 SSLPassword="password-for-key-file" 
 SSLVerifyClient="require"/>
```

## Java system properties {#java-system-properties}

You have the option to set the following two Java system properties to modify the location of configuration and log files for the Primetime DRM Key Server:

* `KeyServer.ConfigRoot` - This directory contains all of the configuration files for the Primetime DRM Key Server. For details on the contents of these files, see [Key Server configuration files](#key-server-configuration-files). If not set, the default is [!DNL CATALINA_BASE/keyserver]. 

* `KeyServer.LogRoot` - This is a log directory that contains iOS Key Server application logs. If not set, the default is the same as `KeyServer.ConfigRoot` 

* `XboxKeyServer.LogRoot` - This is a log directory that contains the Xbox Key Server application logs. If not set, the default is same as `KeyServer.ConfigRoot`.

If you are using [!DNL catalina.bat] or [!DNL catalina.sh] to start Tomcat, these system properties can easily be set using the `JAVA_OPTS` environment variable. Any Java options set here will be used when Tomcat is started. For example, set: 

```
JAVA_OPTS=-DKeyServer.ConfigRoot=”absolute-path-to-config-folder” 
  -DKeyServer.LogRoot=”absolute-path-to-log-folder”
```

## Primetime DRM credentials {#primetime-drm-credentials}

To process key requests from Primetime DRM iOS and Xbox 360 clients, the Primetime DRM Key Server must be configured with a set of credentials issued by Adobe. These credentials can either be stored in PKCS#12 ( [!DNL .pfx]) files or on an HSM.

The [!DNL .pfx] files can be located anywhere, but for ease of configuration, Adobe recommends placing the [!DNL .pfx] files in the tenant's configuration directory. For more information, see [Key Server configuration files](#key-server-configuration-files).

### HSM configuration {#section_13A19E3E32934C5FA00AEF621F369877}

If you choose to use an HSM to store your server credentials, you must load the private keys and certificates onto the HSM and create a *pkcs11.cfg* configuration file. This file must be located in the *KeyServer.ConfigRoot* directory. See the `<Primetime DRM Key Server>/configs` directory for an example PKCS 11 configuration file. For information on the format of [!DNL pkcs11.cfg], see the Sun PKCS11 provider documentation.

To verify that your HSM and Sun PKCS11 configuration files are configured properly, you can use the following command from the directory where the [!DNL pkcs11.cfg] file is located ( [!DNL keytool] is installed with the Java JRE and JDK): 

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

If you see your credentials in the list, the HSM is configured properly and the Key Server will be able to access the credentials.

## Key Server configuration files {#key-server-configuration-files}

The Primetime DRM Key Server requires two types of configuration files:

* A global configuration file, [!DNL flashaccess-keyserver-global.xml] 
* A tenant configuration file for each tenant, [!DNL flashaccess-keyserver-tenant.xml]

If changes are made to the configuration files, the server must be restarted for the changes to take effect.

To avoid making passwords available in clear text in the configuration files, all passwords specified in the global and tenant configuration files must be encrypted. For more information on encrypting passwords, see [*Password Scrambler* in *Using the Primetime DRM Server for Protected Streaming*](../protected-streaming/understanding-deployment/drm-for-protected-streaming-utilities/password-scrambler.md).

## Configuration directory structure {#configuration-directory-structure}

The configuration directories have the following structure: 

```
KeyServer.ConfigRoot/  
--flashaccess-keyserver-global.xml 
--pkcs11.cfg (optional) 
--faxsks/ 
----tenants/ 
------tenantname/
---------flashaccess-keyserver-tenant.xml 
---------credential.pfx (optional) 
```

## Global configuration file {#global-configuration-file}

The [!DNL flashaccess-keyserver-global.xml] configuration file contains settings that apply to all tenants of the Key Server. This file must be located in `KeyServer.ConfigRoot`. See the [!DNL configs] directory for an example global configuration file. The global configuration file includes the following:

* Logging - Specifies the logging level and how frequently log files are rolled. 
* HSM password - Required only if an HSM is used to store server credentials.

See the comments in the example global configuration file located in `<Primetime DRM Key Server>/configs` for more details.

## Tenant configuration files {#tenant-configuration-files}

The [!DNL flashaccess-ioskeyserver-tenant.xml] and [!DNL flashaccess-xboxkeyserver-tenant.xml] configuration files contain settings that apply to a specific tenant of the Primetime DRM Key Server. Each tenant has its own instance of these configuration files located in [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]. See the [!DNL configs/faxsks/tenants/sampletenant] directory for an example tenant configuration file.

You can specify all file paths in the tenant configuration file as either absolute paths or paths relative to the tenant's configuration directory ( [!DNL <KeyServer.ConfigRoot>/faxsks/tenants/tenantname]).

All tenant configuration files include:

* Key Server Credentials - Specifies one or more Key Server credentials (certificate and private key) issued by Adobe. Can be specified as a path to a [!DNL .pfx] file and a password, or an alias for a credential stored on an HSM. Several such credentials can be specified here, either as file paths, or key aliases, or both.

The **iOS** tenant configuration file includes:

* Key Delivery Window - (Optional) Specifies key delivery request timestamp validity window (in seconds). Default value is 500 seconds.

The **Xbox 360** tenant configuration file includes:

* XSTS Credential - Specifies the application developer's credential used to decrypt XSTS tokens 
* XSTS Signing Certificate - Specifies the certificate used to verify the signature on XSTS tokens. 
* Packager Allow list - Packager certificates that are trusted by the Key Server. If there are no packager certificates contained in the list, then all packager certificates will be trusted.

## Log files {#log-files}

The log files generated by the Primetime DRM Key Server application ( [!DNL flashaccess-ioskeyserver_*.log] and [!DNL flashaccess-xboxkeyserver_*.log]) will be located in the directory specified by `KeyServer.LogRoot`.

The log files are distinguished by client type. There are two logs per client type:

* An *access log* - Monitors requests and responses only. 
* A *context log* - Contains detailed error messages and stack traces.

## Starting the Key Server {#starting-the-key-server}

To start the Key Server, start Tomcat.
