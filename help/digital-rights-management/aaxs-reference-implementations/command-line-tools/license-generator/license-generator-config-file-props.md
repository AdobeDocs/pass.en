---
title: Configuration File Properties
description: Configuration File Properties
copied-description: yes
exl-id: ce4193fa-d217-4134-b08e-715c2cc57c84
---
# Configuration File Properties {#configuration-file-properties}

Before you run the License Generator, specify values for the License Generator properties. The configuration file specifies the following properties. For property names that include *n*, *n* represents an integer starting with 1 and increasing for each instance of the property. 

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_qk1_rry_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> Property </th> 
   <th colname="2" class="- topic/entry entry"> Description </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.minClientVersion</span> </td> 
   <td colname="2" class="- topic/entry "> Set the minimum client version supported. If not set, by default all versions are supported. Set this value to control how older clients respond to license requirements that they do not support. Specify x (for Adobe Access x.0) where x is the major release number. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keyServerCert</span> </td> 
   <td colname="2" class="- topic/entry "> Key Server Certificate (an Adobe-issued License Server certificate used by the Key Server). This certificate is used only if the metadata/policy indicates that a Key Server is required for key delivery to iOS devices. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile</span> </td> 
   <td colname="2" class="- topic/entry "> The PKCS12 file containing the License Server credentials for signing licenses. This property should refer to a .pfx file containing a certificate and private key. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certpass</span> </td> 
   <td colname="2" class="- topic/entry ">The password used to protect the file specified by <span class="+ topic/ph pr-d/codeph codeph"> licensegen.sign.certfile.</span> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.domainca.n</span> </td> 
   <td colname="2" class="- topic/entry "> If generating domain-bound licenses, one or more Domain CA certificates must be specified to indicate the domain authorities trusted by this license issuer. If the license recipient is a domain certificate, which was not issued by one of the specified Domain CAs, a license cannot be generated. This property specifies a .cer file that contains the certificate only (either PEM or DER format is acceptable). n must be monotonically increasing, starting from 1. </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymmetric.licenseServerCredential.n</span> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Optional PKCS12 file containing additional License Server credentials for decrypting the CEK in the metadata and policy. Additional credentials may be configured if content was previously packaged with a License Server certificate other than that specified by <span class="codeph"> licensegen.sign.certfile</span>. This property should refer to a <span class="filepath"> .pfx</span> file containing a certificate and private key. n must be monotonically increasing, starting from 1. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "><span class="+ topic/ph pr-d/codeph codeph">licensegen.keys.asymmetric.licenseServerCredential.n.password</span> </td> 
   <td colname="2" class="- topic/entry ">The password used to protect the file specified by: <p><span class="+ topic/ph pr-d/codeph codeph"> licensegen.keys.asymmetric.licenseServerCredential.n</span> </p> </td> 
  </tr> 
 </tbody> 
</table>
