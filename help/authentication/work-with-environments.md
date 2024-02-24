---
Title: Work with environment
Description: Understand the use and working with different environments of TVE dashboard.
---
# Work with environments {#work-with-authn-environments}

Environments are the different conditions where a program or system operates, customized to fulfill specific purposes. The TVE Dashboard has two primary environments:

* **Prequal**: The Pre-qualification environment serves as a testing ground for preparing and testing new builds before deployment to the live environment.

* **Release**: The Release environment hosts the finalized and tested builds for production use.

Within each environment, there are two different profiles: 

* **Staging**: The staging profile connects to MVPD's staging server for testing and validation of integrations before going live.

* **Production**: The production profile connects to MVPD's production server for actual production activities and provides authentication services to programmers. 

## Uses at a glance

The environments and profiles in the TVE Dashboard serve various use cases throughout the application lifecycle. These environments allow you to:

### Prequal Staging

* Validate new, unreleased features of the Adobe Authentication server using MVPD's staging endpoints.
* Primarily used by Adobe Authentication product team for adding and validating new MVPD integrations.

### Prequal Production

* Validate new, unreleased features or configurations of the Adobe Authentication server using MVPD's production endpoints.
* Acts as the environment to validate every configuration change before pushing it to release production.

### Release Staging

* Validate new application versions for each channel using MVPD's staging endpoints.
* Conduct performance or capacity tests within this environment.

### Release Production

* Represents the "live" environment with the latest Adobe Pass release build available to programmers.
* Maintains stability in code and configuration by immediately reflecting changes on the programmer's application.

For detailed information on the Adobe Pass Authentication environments, view [Understanding the Adobe Pass Authentication environments](/help/authentication/understanding-the-adobe-environments.md).

## Switch environments {#switch-environments}

>[!NOTE]
>
> The configurations may vary in each environment based on your settings.

To switch between Adobe Pass Authentication environments:

1. Log in with your authorized programmer credentials.
1. Select the **Environment** tab at the top of the left panel.
1. Choose the desired environment from the drop-down menu.

![TVE Dashboard environments dropdown](assets/tve-dashboard-env.png)

*Figure: The Adobe Pass TVE Dashboard environments drop-down* 


<!--Remove this section
>[!IMPORTANT]
>
>When making administrative changes to your Adobe Pass Authentication configuration through the TVE Dashboard, we strongly advise you to follow the sequence below in order to ensure proper functionality.

To make administrative changes to your Adobe Pass Authentication configuration through the TVE Dashboard:

* Perform the changes in [Release Staging and validate them](http://sp.auth-staging.adobe.com/apitest/api.html).
* Perform the changes in [Prequal Production and validate them](http://sp.auth-staging.adobe.com/apitest/api.html).
* Perform the changes in [Release Production and validate them](http://sp.auth-staging.adobe.com/apitest/api.html). -->

<!--Remove this section
For the administrative changes to go live, navigate to **Review and Push Changes** section by selecting the button, which will show up in the bottom-left part of the sidebar, in order to review changes, add a description for the newly created changes and confirm the configuration update by selecting the "Push Configuration".

![Tve Dashboard review an push notification](assets/tve-review-push-notifications.png)

*Figure: The Adobe Primetime TVE Dashboard Review and Push Changes notification*-->

