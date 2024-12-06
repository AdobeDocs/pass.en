---
title: REST API V2 Overview
description: REST API V2 Overview
exl-id: a5595193-82c4-4033-bd98-596b4908b401
---
# REST API V2 Overview {#rest-api-v2-overview}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

Do you want to improve the cost efficiency of your TVE applications?

Do you want to reduce the development time and resources required to support TVE applications on multiple platforms?

Do you want to ensure a consistent user experience across platforms?

Do you want to reduce maintenance effort and simplify providing updates, bug fixes, or improvements?

## Introducing REST API V2

Adobe Pass Authentication is thrilled to announce the launch of REST API V2, designed to enhance user experience and simplify integration with Pass services.

We are excited about the possibilities of our new REST API, which represents a major step forward for our platform and opens the door for new features and application flows.

## What’s New?

Unique implementation across all platforms

Customers' applications can now use the same implementation across platforms, making it easier to launch new features or maintain live apps.

### Cross-device SSO

REST API V2 allows an authentication session to be securely passed between different devices. By simply passing the session between devices, users can authenticate on their mobile device and stream video on a TV-connected device without re-authentication.

### Multiple active authentication sessions

Different active MVPD sessions are now possible, and customers can choose to switch between TempPass and regular MVPD integration when needed.

### Enhanced security mechanism

Dynamic Client Registration is the security mechanism used across all flows and functionalities. It allows for more secure and granular control of customers' applications and can register applications on all platforms.

### Improved performance for faster response times

Enhanced caching mechanisms allow for less traffic to MVPDs, improving response times and reducing latency. Overall, there is a reduced number of API calls until the video starts.

### Enhanced error codes on all flows

Advanced error codes are now available on all Pass flows in the same format, with additional details guiding the applications to improve the overall user experience.

### Improved control over all authentication sessions

The new REST API V2 permits actions on multiple authenticated sessions at the same time.

### Reduce maintenance costs

All responses and error information are now normalized.

## What’s Next?

All customers currently using our APIs through SDKs or REST calls can continue to do so, as we plan to continue providing support through the end of 2025.

However, all future developments will be built on the REST API V2. We strongly recommend starting the migration process to benefit from the latest Adobe Pass functionalities.

## Want to learn more?

To get started, visit our public documentation:

- [Glossary](rest-api-v2-glossary.md)
- [FAQs](rest-api-v2-faqs.md)
- [APIs](apis/rest-api-v2-apis-overview.md)
- [Flows](flows/rest-api-v2-flows-overview.md)
- Cookbooks
- Appendix
- [Minimum System Requirements](/help/authentication/integration-guide-programmers/minimum-system-requirements.md)

Our dedicated support team is also available to help you with any questions or technical assistance you may need.

## Want to try the REST API V2?

You can now explore the REST API V2 through our product-dedicated page from [Adobe Developer](https://developer.adobe.com/adobe-pass/) website.
