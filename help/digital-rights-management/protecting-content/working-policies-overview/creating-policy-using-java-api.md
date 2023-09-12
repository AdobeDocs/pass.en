---
title: Creating a DRM policy with the Java API
description: Creating a DRM policy with the Java API
copied-description: yes
exl-id: fcae76c3-4e51-449d-b6d5-2138bf1c583e
---
# Creating a DRM policy with the Java API {#creating-a-drm-policy-with-the-java-api}

To create a DRM policy with the Java API:

1. Set up your development environment and include in your project all of the JAR files listed in [Set up your development environment.](../../protecting-content/setting-up-the-sdk/setup-dev-env.md). 
1. Create a `com.adobe.flashaccess.sdk.policy.Policy` object and specify its properties, including the rights, license caching duration, and DRM policy end date. 

   ```java
   // Create a new DRM policy object.  
   // False indicates the DRM policy does not use license chaining.  
   Policy policy = new Policy(false);  
     
   policy.setName("DemoPolicy");  
     
   // Specify that the DRM policy requires authentication to obtain a license.  
   policy.setLicenseServerInfo(new LicenseServerInfo(AuthenticationType.UsernamePassword));  
     
   // A DRM policy must have at least one Right, typically the play right  
   PlayRight play = new PlayRight();  
     
   // Users can only view content for 24 hours.  
   play.setPlaybackWindow(24L * 60 * 60);  
     
   // Add the play right to the DRM policy.  
   List<Right> rightsList = new ArrayList<Right>();  
   rightsList.add(play);  
   policy.setRights(rightsList);  
     
   // Licenses can be stored on the client for 7 days after downloading  
   policy.setLicenseCachingDuration(7L * 24 * 60 * 60);  
   try {  
       // Content will expire December 31, 2010  
       SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd");  
       policy.setPolicyEndDate(dateFormat.parse("2010-12-31"));  
   } catch (ParseException e) {  
       // Invalid date specified in dateFormat.parse()  
       e.printStackTrace();  
   } 
   
   ```

1. Serialize the DRM `Policy` object and store it in a file or database. 

   ```java
   // Serialize the DRM policy  
   byte[] policyBytes = policy.getBytes();  
   System.out.println("Created DRM policy with ID: " + policy.getId());  
         
   // Write the DRM policy to a file.   
   // Alternatively, the DRM policy may be stored in a database.  
   FileOutputStream out = new FileOutputStream("demopolicy.pol");  
   out.write(policyBytes);  
   out.close(); 
   
   ```

See [!DNL com.adobe.flashaccess.samples.policy.CreatePolicy] in the Reference Implementation Command Line Tools [!DNL samples] directory for the complete source of this sample code.
