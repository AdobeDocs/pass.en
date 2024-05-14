---
title: TVE Dashboard environments
description: Understand the use and working of different environments in the TVE Dashboard.
---
# Environments {#environments}

>[!NOTE]
>
>The content on this page is provided for information purposes only. The usage of this API requires a current license from Adobe. No unauthorized use is permitted.

The TVE Dashboard provides different environments customized to fulfill specific purposes within the Adobe Pass Authentication. There are two primary environments:

* **Prequal**: The pre-qualification environment serves as a testing ground for preparing and testing new builds before deployment to production.

* **Release**: The release environment hosts the finalized and tested builds for production.

Within each environment, there are two different profiles:

* **Staging**: The staging profile connects to the MVPD's staging server for testing and validation of integrations before going live.

* **Production**: The production profile connects to the MVPD's production profile for actual production activities.

## Use cases

The environments in the TVE Dashboard serve various use cases throughout the application lifecycle. These environments allow you to:

### Prequal Staging

* Validate new unreleased features of the Adobe Pass Authentication server using MVPD's staging endpoints.
* Primarily used by the Adobe Pass Authentication product team to add and validate new MVPD integrations.

### Prequal Production

* Validate new unreleased features or configurations of the Adobe Pass Authentication server using MVPD's production endpoints.
* Validate new application versions for each channel using MVPD's production endpoints.
* Validate every configuration change before pushing it to production.

### Release Staging

* Validate new application versions for each channel using MVPD's staging endpoints.
* Conduct performance or capacity tests within this environment.

### Release Production

* Represents the live environment with the latest Adobe Pass release build generally available to all end users.
* Maintains stability in code and configuration and immediately reflects configuration changes in the end user's application.

## Switch environments {#switch-environments}

Follow the steps to switch between Adobe Pass Authentication TVE Dashboard environments.

1. Log in with your programmer credentials.
1. Select the required staging or production environment from the **Environment** dropdown menu at the top of the left panel.

   ![TVE Dashboard environments dropdown](assets/tve-dashboard-env.png)

   *The Adobe Pass Authentication TVE Dashboard environment dropdown menu*

>[!NOTE]
>
> The configurations may vary in each environment based on your settings.

