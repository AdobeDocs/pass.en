---
title: About CRL Files
description: About CRL Files
copied-description: yes
exl-id: 126a323d-9433-4a1e-a617-2d3bbf717cce
---
# About CRL Files {#about-crl-files}

In order to properly function, Individualization and License servers need to have several Certificate Revocation List (CRL) files cached to disk on the running application server (e.g., Tomcat). New CRL files have to be downloaded and cached on disk on a regularly scheduled basis. If the validity period of CRL files on disk are allowed to lapse, the Individualization Server will refuse to individualize clients, and the License Server will refuse to issue licenses.

The CRLs cached to disk must have file names that match the corresponding URLs. Special characters such as colons ':' and '/' slashes are converted to underscores '_' in the file names.

The following is a list of externally hosted CRLs that are used by both the Individualization and License Servers:

* **Intermediate CRL:**

  * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessIntermediateCA.crl>]
  * File: [!DNL http___crl2.adobe.com_Adobe_FlashAccessIntermediateCA.crl]
  * Validity: Good for approximately 12 months from creation

* **Root CRL:**

  * URL: [!DNL <ht<span></span>tps://crl2.adobe.com/Adobe/FlashAccessRootCA.crl>]
  * File: [!DNL http___crl2.adobe.com_Adobe_FlashAccessRootCA.crl]
  * Validity: Good for approximately 5 years from creation

* **Latest CRL:**

  * URL: [!DNL <ht<span></span>tps://crl3.adobe.com/AdobeSystemsIncorporatedFlashAccessRuntime/LatestCRL.crl>]
  * File: [!DNL http___crl3.adobe.com_AdobeSystemsIncorporatedFlashAccessRuntime_LatestCRL.crl]
  * Validity: Good for approximately 3 months from creation

To know about the externally hosted CRLs that can be used by the License Servers, contact Adobe Support.

<!---

Commenting out because of a security vulnerability reported in Jira PSIRT-20689. 

The following are externally hosted CRLs that are used only by the License Servers:

* URL: `https://crl2.adobe.com/Adobe/FlashAccessIndividualizationCA.crl`

* File: `http___crl2.adobe.com_Adobe_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

* URL: `https://individualization-crl.primetime.adobe.com/FlashAccessIndividualizationCA.crl`

* File: `http___individualization-crl.primetime.adobe.com_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

* URL: `https://individualization-crl.s3-website-us-east-1.amazonaws.com/FlashAccessIndividualizationCA.crl`

* File: `http___individualization-crl.s3-website-us-east-1.amazonaws.com_FlashAccessIndividualizationCA.crl`

* Validity: Good for approximately 3 months from creation

--->

In addition to the externally hosted CRLs, you can create and maintain an additional CRL. This is the Individualization CA CRL, as specified in the [Create Individualization CA CRL](../../../on-premises-i15n-server/server-configuration-section/server-properties/create-i15n-ca-crl.md) section of this document.

CRLs are scheduled to be updated 45 days before they are to expire. This should allow you adequate time to acquire and install newly generated CRLs from the Internet. You must take care to update CRL files before they are expired.
