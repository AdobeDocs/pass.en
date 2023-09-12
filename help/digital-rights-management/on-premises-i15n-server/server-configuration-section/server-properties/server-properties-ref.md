---
title: Server Properties Reference
description: Server Properties Reference
copied-description: yes
exl-id: 8724d097-7cba-4ca9-b597-df56f80b2e9c
---
# Server Properties Reference{#server-properties-reference}

<!--<a id="section_EC8810492A454BDBA6013FE376360F4E"></a>-->

## Individualization Server

<table id="table_ats_tk2_jr">  
 <thead> 
  <tr> 
   <th class="entry"> Configuration </th> 
   <th class="entry"> Description </th> 
   <th class="entry"> Example </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> Transport Credential </td> 
   <td>The transport credential is used to decrypt requests received from the client and sign the responses sent back. Be sure to configure the <span class="filepath"> AdobeInitial.properties</span> file appropriately with both the path to the transport credential file, as well as the encrypted PKCS12 password. </td> 
   <td> 
    <ul id="ul_itx_fl2_jr"> 
     <li id="li_A2E65253F37245268A41E6B9C958C8DF"><span class="codeph"> cert.i15n.transport.file = </span> [PKCS12 file containing the Individualization Transport cert and key] </li> 
     <li id="li_28CDFC0B3D684795AF4708B6D26DF83F"><span class="codeph"> cert.i15n.transport.password =</span> [Encrypted password for PKCS12 file] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Individualization CA Credential </td> 
   <td>The Individualization server uses the Individualization CA credential to sign the machine certificates that it issues. Be sure to configure the <span class="filepath"> AdobeInitial.properties</span> file appropriately with both the path to the I15N CA credential file, as well as the encrypted PKCS12 password. </td> 
   <td> 
    <ul id="ul_xsj_nl2_jr"> 
     <li id="li_5A770D8A482F41A4A9AB63CA52C2EB90"><span class="codeph"> cert.i15n.ica.file =</span> [PKCS12 file containing the Individualization CA cert and key] </li> 
     <li id="li_C3C4A2D9AA2A4F86B6DDCFFD9CB55CBB"><span class="codeph"> cert.i15n.ica.password =</span> [Encrypted password for PKCS12 file] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Individualization Encryption Credential </td> 
   <td> The Individualization server uses the Encryption credential to encrypt sensitive files that need to be transmitted to the Individualization servers. For example, this cert supports license migration and is also used to encrypt the DRM private keys for the Individualization servers. </td> 
   <td> 
    <ul id="ul_nbr_kpd_w5"> 
     <li id="li_4226AD6CC85740669DAF467EFD00BBBE"><span class="codeph"> cert.i15n.decryption.file=i15n_transport.pfx</span> </li> 
     <li id="li_F51BDD94F4724FA58CEF9470B6FEE33B"><span class="codeph"> cert.i15n.decryption.password=password</span> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Content Cache </td> 
   <td>These settings control the location from which the Individualization server downloads content and where the content is cached on disk. The Individualization server will check the content server for new content once at startup, then at the frequency/time specified by these properties. <p>For the On Premises Individualization Server, we have included an initial set of content cache data. Be sure to copy the <i>CONTENTS</i> of the cache folder (not the cache folder itself) to the configured <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> contentServer.localDirectory</span> location. </p> </td> 
   <td> 
    <ul id="ul_r4n_1r2_jr"> 
     <li id="li_CA5F562577B04B4A9966EF46E039A137"><span class="codeph"> contentServer.localDirectory =</span> [Directory in which to store local content (normally tomcat/temp)] </li> 
     <li id="li_9A78FBD6C54D47708226378340B46E8E"><span class="codeph"> contentServer.server =</span> [Web server to contact for ECI info (<i>unsupported in this release</i>)] </li> 
     <li id="li_4E7D7F76085D411688B5003E855F860B"><span class="codeph"> contentServer.timeout =</span> [Connection timeout, in seconds] </li> 
     <li id="li_4B751F238A1643A7AC730CD9354887B6"><span class="codeph"> contentServer.pollFrequency =</span> [How frequently to poll the server, in days (minimum is 1 day)] </li> 
     <li id="li_8E23C3C6E7EF46B0AFDD7993DE79F142"><span class="codeph"> contentServer.pollTime =</span> [Time of day to poll the server, in minutes since midnight] </li> 
    </ul> <p>Please be sure to read the section <i>CRL and ECI Files</i> about keeping the cache up to date. </p> </td> 
  </tr> 
  <tr> 
   <td> Individualization CA CRL </td> 
   <td> <p>This Certificate Revocation List (CRL) distribution point is included within each machine certificate issued by the Individualization server. During machine certificate validation on the license server, the CRL will be downloaded from the distribution point listed in the certificate (or read from the cache if already downloaded) and checked to be sure the certificate has not been revoked. It is recommended to perform this server configuration change after going through the process of creating and deploying the Individualization CA CRL. Restart the Individualization server after any configuration change. </p> <p>To set the URL for the CRL distribution point, you will need to set the <span class="filepath"> AdobeInitial.properties</span> <span class="codeph"> cert.machine.crldp</span> field. </p> </td> 
   <td> 
    <ul id="ul_eq3_lv2_jr"> 
     <li id="li_5E37A9E318D742B6A5E1035120888819"><span class="codeph"> cert.machine.crldp =</span> [CRL distribution point] </li> 
    </ul> <p>For example: </p>
    <p> <code>
      cert.machine.crldp__DEV=<span>tps://onprem-individualization.com</span>CRL/onprem-individualization-ca.crl
     </code></p>
     <p>The License Server should automatically download this CRL, once a license request is handled. </p> <p importance="high">Note: This distribution point is <i>not</i> checked by Primetime DRM for validity. You must verify that this URL is valid. Errors resulting from an invalid URL will not appear until validation errors appear from the license server. </p> </td> 
  </tr> 
  <tr> 
   <td> Logging </td> 
   <td>Configure the <span class="filepath"> AdobeInitial.properties</span> for logging as necessary. </td> 
   <td> 
    <ul id="ul_j1v_kw2_jr"> 
     <li id="li_B60002B33A3042FCBE1F694454966469"><span class="codeph"> adobe.weblogs.loc =</span> [Directory where log files will be created] </li> 
     <li id="li_2DD4406FBBF047589BAAAE1C9082D8B3"><span class="codeph"> log.Level =</span> [The lowest level of log messages which may appear in the logs <span class="codeph"> [DEBUG | INFO]</span> ] </li> 
     <li id="li_610FAF239A554CE59DAC455174F0CF0A"><span class="codeph"> log.FileName =</span> [Prefix for log files. Date/time and ".log" extension will be added to the filename] </li> 
     <li id="li_1F2913B209BE4A0E8207FAAD052D1764"><span class="codeph"> log.RollInterval =</span> [Specifies how frequently the logs are rolled.] </li> 
     <li id="li_3F46C15488114BB5B41035F710E7A19F"><span class="codeph"> log.RollSize =</span> [Roll the logs when they reach this size (Logs will roll when either the <span class="codeph"> RollInterval</span> or <span class="codeph"> RollSize</span> is reached, whichever comes first)] </li> 
     <li id="li_DA32E862F7B0413885DA20633B682484"><span class="codeph"> log.ReportLogging.Enabled =</span>[ [true | false ] Specifies whether a separate file should be generated which contains data used by Adobe to generate Individualization reports.] </li> 
     <li id="li_465CC6D81B8A484CBF4E7A39F7AF86AA"><span class="codeph"> log.ReportLogging.FileName =</span> [Prefix for report log files. Date/time and <span class="filepath"> .log</span> extension will be added to the filename. The l<span class="codeph"> og.Level</span> property does not apply to this log file, but <span class="codeph"> log.RollInterval</span> and <span class="codeph"> log.RollSize</span> do.] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Other </td> 
   <td></td> 
   <td> 
    <ul id="ul_b3b_g1f_jr"> 
     <li id="li_FACF07CB332D416E91FD34DE48152FAA"><span class="codeph"> deviceinfo.key =</span> [Encrypted Base64 encoded key used to HMAC device info before including it in the machine token. The key can be different for the Dev/Staging/Production environments, but must be the same for all servers in a particular environment. ] </li> 
     <li id="li_B19C77FD6F91496294DBF836A1922EE1"><span class="codeph"> keys.kgs.server =</span> [Location of Key Gen Server (a single host/port, representing a pool of key servers) ] </li> 
     <li id="li_5DA3C89770804B148EF6FAF01A5AD958"><span class="codeph"> keys.MinQueueSize =</span> [Fetch another batch of keys from the KGS when there are this many keys left in the queue] </li> 
     <li id="li_0C2E5F2FDB824182A6BE418B041D2F28"><span class="codeph"> status.Timeout =</span> [Status page will ping the KGS to determine if it can reach the server. It will time out if a response isn't received back in the specified amount of time.] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Key Generation Server {#section_37FA8EEBA258461F8CFA3ADF37714577}

<table id="table_ats_tk2_js"> 
 <thead> 
  <tr> 
   <th class="entry"> Configuration </th> 
   <th class="entry"> Description </th> 
   <th class="entry"> Example </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> Key Generation </td> 
   <td></td> 
   <td> 
    <ul id="ul_nlj_ydf_jr"> 
     <li id="li_E4347D572F004BF0B237A662BFE7F3ED"><span class="codeph"> kgs.Threads =</span> [Number of threads to use to generate keys (should equal the number of processors available on the machine)] </li> 
     <li id="li_EDBC2535D48E4A66AEB240DB337187FC"><span class="codeph"> kgs.BatchSize =</span> [Number of keys to generate per batch] </li> 
     <li id="li_07B41546D94F42349103BF8AF4605E14"><span class="codeph"> kgs.KeyDirectory =</span> [Directory in which to store key batch files] </li> 
     <li id="li_F4962C97DC3D491DA7FAC826E38A4459"><span class="codeph"> kgs.MaxQueueSize =</span> [Maximum number of key batch files to generate] </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> Logging </td> 
   <td></td> 
   <td> 
    <ul id="ul_kwq_12f_jr"> 
     <li id="li_5E5D34FE5EB44BB898090494C7DDEBD8"><span class="codeph"> adobe.weblogs.loc =</span> [Directory where log files will be created] </li> 
     <li id="li_0E34CD32CD5E47729B69B50414F93678"><span class="codeph"> log.FileName =</span> [Prefix for log files. Date/time and <span class="filepath"> .log</span> extension will be added to the filename] </li> 
     <li id="li_8AB15ACEC39041A2A04C7301154C6EDB"><span class="codeph"> log.Level =</span> [The lowest level of log messages which may appear in the logs] </li> 
     <li id="li_A17E84DA3ED243F381FF3A6184A3CAA0"><span class="codeph"> log.RollInterval =</span> [Specifies how frequently the logs are rolled.] </li> 
     <li id="li_C2B3D111608945DA9D1428BE98D61664"><span class="codeph"> log.RollSize =</span> [Roll the logs when they reach this size (Logs will roll when either the <span class="codeph"> RollInterval</span> or <span class="codeph"> RollSize</span> is reached, whichever comes first)] </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
