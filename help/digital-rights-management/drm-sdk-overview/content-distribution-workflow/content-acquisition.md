---
description: When a consumer acquires a protected content file from a website or CDN, the consumer must also acquire a license that contains a key to decrypt the video before it can be played. The following steps illustrate a common workflow for how protected content is accessed by a computer running Flash Player or Adobe AIR 
title: Content acquisition
exl-id: 92d51928-6021-4284-9310-4e6ce758bffc
---
# Content acquisition{#content-acquisition}

When a consumer acquires a protected content file from a website or CDN, the consumer must also acquire a license that contains a key to decrypt the video before it can be played. The following steps illustrate a common workflow for how protected content is accessed by a computer running Flash Player or Adobe AIR:

1. The consumer visits the retailer's website, and selects a video to watch. The consumer attempts to download or stream the protected video to their computer using either Flash Player or an Adobe AIR application.

   If this is the first time the consumer has attempted to access protected content using this specific computer, the Flash Player or Adobe AIR runtime must first be individualized as described in Step 2. If the runtime client has already been individualized, the process of acquiring a license occurs as described in Step 3. 

1. The Flash Player or Adobe AIR runtime client acquires a unique digital certificate (called a *machine certificate*) from an Adobe-hosted server.

   This process of assigning a unique certificate is called *individualization*. Individualization uniquely identifies both the computer and the Flash Player or Adobe AIR runtime used to playback content.

   The individualization process allows the downloaded licenses to be bound to a specific computer on which the client is installed. Every computer is given a unique machine credential (machine private key and machine certificate). If a specific client were to become compromised, it can be revoked and barred from acquiring licenses for new content. 

1. The client parses the protected content as it begins to download or stream to the consumer's computer, and extracts the URL of the retailer's License Server from the Primetime DRM metadata embedded within the file.

   The Primetime DRM metadata is typically separate from the content, such as embedded in an accompanying manifest file or as a binary blob, but can also be embedded within the content file. The client contacts the License Server at the specified URL, and acquires a license (as described below in Step 4).
1. The client acquires a license from the retailer's License Server.

   During license acquisition, the client sends information identifying the requested content (the *Primetime DRM metadata*) and the machine certificate (identifying the consumer's computer) to the retailer's License Server. The license request sent to the server is encrypted using the Transport public key, which is also included in the Primetime DRM metadata.

   The License Server — which may be integrated into the retailer's billing and authentication infrastructure — can perform a business rules check to verify that the user is authorized to view the requested content. If the business rules allow it, the License Server issues a license containing the content encryption key to decrypt the content and the usage rules associated with that user's account. To process a license request, the License Server decrypts the request using its Transport private key. The CEK in the metadata is decrypted using the License Server private key, and re-encrypted to bind the license to the device making the request. The license is signed using the License server private key. The license response is signed using the Transport private key, and encrypted before being returned to the client.

   If allowed by the license, the client stores the license to enable *offline access* to the license. License caching allows the consumer to view protected content without reacquiring a license every time they want to view content. 

1. Once the Flash Player or Adobe AIR runtime client has a license, the client extracts the CEK from the license, and the consumer can view the content they are authorized to access.

   <!--<a id="fig_s43_gc2_44"></a>-->

   ![](assets/FMRMS_fig01_web.png)

   The previous example shows just one possible workflow. Alternatively, you might use a workflow with a proactive download of content where the license acquisition happens much later. Another option is to implement a pre-order workflow where the license acquisition occurs before the content is accessed.
