---
description: The TVSDK Primetime Reference is an Android application built around the TVSDK and AVE frameworks.
title: Build the Primetime reference implementation
exl-id: d2950f2b-06d7-4fc8-a031-5f058ce47545
---
# Build the Primetime reference implementation {#build-the-primetime-reference-implementation}

The TVSDK Primetime Reference is an Android application built around the TVSDK and AVE frameworks.

To set up and build the Primetime Reference project in Eclipse: 

1. Download the TVSDK Android zip file and unpack it into a directory in a location that you will remember.
1. Launch Eclipse.
1. Select **[!UICONTROL File]** > **[!UICONTROL Import]**.
1. Select **[!UICONTROL Android]** > **[!UICONTROL Existing Android Code Into Workspace]**.
1. Click **[!UICONTROL Next]**.
1. Use the **[!UICONTROL Browse]** button to populate the **[!UICONTROL Root Directory]** field with the directory under [!DNL samples/PrimetimeReference/src] to which you unpacked the TVSDK Android zip file.
1. Select the following projects to import: **[!UICONTROL appcompat]**, **[!UICONTROL PrimetimeReference]**.
1. Click **[!UICONTROL Finish]**.
1. Select  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** to build the project.

   This step is not necessary if the project is set up to build automatically.
1. If you would like to include the tests project in the workspace, associate the tests project with the PrimetimeReference project:
   1. Repeat steps 3. through 6.
   1. Select the following project to import: `PrimetimeReference\tests`.
   1. Click **[!UICONTROL Finish]**.
   
      The tests project has a dependency on the CatalogActivity project so you need to associate the tests project with the CatalogActivity project.   
   1. Right-click **[!UICONTROL tests]** and choose **[!UICONTROL Properties]**.
   1. Select the **[!UICONTROL Projects]** tab under Java Build Path.
   1. Click **[!UICONTROL Add...]**
   1. Select CatalogActivity.
   1. Click **[!UICONTROL OK]** to add the project.
   1. Click **[!UICONTROL OK]** to exit the Properties page.
   1. Select  **[!UICONTROL Project]** > **[!UICONTROL Build Project]** to build the project.
   
      This step is not necessary if the project is set up to build automatically.
