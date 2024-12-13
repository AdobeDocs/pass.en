---
title: Understanding the Adobe Environments
description: Understanding the Adobe Environments
exl-id: bb6cf37f-48cd-47bb-b3c2-f7a96e49b12d
---
# Understanding the Adobe Environments {#understanding-the-adobe-environments}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

The official documentation describing the Adobe environments is available [Setting up your environment and testing in Pre-qual](/help/authentication/notes-technical/environments/setting-up-your-environment-and-testing-in-prequal.md):

The Adobe environments, summed up in a few words:

Adobe has two environments: **Pre-Qualification** and **Release**.

* On the Pre-qualification environment we're preparing the new build to be released.

* The current release build is on the Release environment.

Each environment has two profiles : **staging** and **production**.

* The staging profile connects to the MVPDs staging server
* The production profile connects to the MVPDs production profile.

The reason for having the two profiles is that on the staging profile we're preparing new partners to go live, and they would like to test the system with either the upcoming build (Pre-Qualification) or with the release one (more stable).

If a partner wants to test the new version there are a couple of additional steps that need to be done. See, [Setting up your environment and testing in Pre-qual](/help/authentication/notes-technical/environments/setting-up-your-environment-and-testing-in-prequal.md).

By following the steps above, it is assured that the upcoming release will be tested in the Pre-qualification environment.
