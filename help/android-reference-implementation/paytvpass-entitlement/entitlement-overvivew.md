---
description: The Entitlement Manager is the feature manager that supports the Primetime authentication implementation.
title: Entitlement Manager Overview
exl-id: a66e131e-283f-4378-b834-7cfa887b3ec9
---
# Entitlement Manager Overview {#entitlement-manager-overview}

The Entitlement Manager is the feature manager that supports the Primetime authentication implementation.

## Feature Overview

The Primetime authentication integration with the Android Primetime SDK Reference Implementation adds a new feature manager to the application. However, unlike many of the other feature managers, *the EntitlementManager is used in several places throughout the application*. The following provides an overview of the changes and additions made to the Reference Implementation to support Primetime authentication:

### EntitlementManager class

The `EntitlementManager` class handles all the communication with the Primetime authentication SDK, plus encapsulates the application logic required for the entitlement workflows. The `EntitlementManager`'s public API is used by the application to initiate entitlement workflows, while the `EntitlementMangerListener` interface provides a callback mechanism for the application to handle `EntitlementManger` events. 

### EntitlementManger callbacks

The Reference Implementation's main activity, the `CatalogActivity`, creates an instance of `EntitlementManagerListener` and registers it with the `EntitlementManager`. In this way, the `EntitlementManager` may signal needed UI updates to the rest of the application. The callbacks include displaying/hiding a loading dialog, displaying status dialogs, updating authorization and authentication icons, and starting video playback upon successful authorization. 

### Entitlement Dialogs

The `EntitlementDialogFragment` class generates dialog messages based on the entitlement status passed to the class constructor. This class is used for authentication success messages as well as all error messages. The `CatalogActivity` displays the entitlement dialogs when it receives specific events from the `EntitlementManager`. In addition, the `CatalogActivity` implements the `EntitlementDialogListener` interface, which includes callback methods to signal when a dialog is closed or when the user logs out from the Primetime authentication service. 

### Content Provider Selection and Login

During authentication with Primetime authentication, two new activities, `MvpdPickerActivity` and `MvpdLoginActivity`, allow the user to select their content provider and login. Both of these activities are started from the `CatalogActivity` via the `EntitlementManager`. Additionally, both the `MvpdPickerActivity` and `MvpdLoginActivity` return results to the `CatalogActivity` and therefor the `CatalogActivity` must override the `Activity.onActivityResult` method. 

### Sign In button

The Reference Implementation's main activity, the `CatalogActivity`, includes a new "Sign In" button in its action bar. The Sign In button allows the user to initiate authentication with Primetime authentication. Additionally, the user may initiate authentication by selecting a protected video for playback. The Sign In button's icon and text changes depending on the user's authentication status, and the `CatalogActivity` contains code to update the button's icon and text when the page refreshes. To do this, when the `CatalogActivity` starts, it calls `EntitlementManager.checkAuthentication()` to update the user's authentication status. 

### Content entitlement

Within the `CatalogView`, new icons are displayed on top of the content's icon to signal the user's authorization status for that content. For example, if the user is pre-authorized to view a video, then a green circle icon is displayed over the content. However, if the user is not pre-authorized to view the video, a key icon is displayed. The display of these icons is handled in `ContentTileAdapter`, however the update of their state is initiated from the `CatalogActivity` when a callback in the `EntitlementManagerListener` is called. 

### Content Playback

Video playback now requires an authorization check by the `EntitlementManager`. The call to `EntitlementManager.getAuthorization()` occurs within `CatalogView`. If the video requires authorization and the user is authorized, the `PlayerActivity` is started from the `CatalogActivity`.
