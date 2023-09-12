---
title: Creating a policy using the Java API
description: Creating a policy using the Java API
copied-description: yes
exl-id: 60e26fd6-1b72-413c-a35b-b317389cd9ed
---
# Creating a policy using the Java API {#creating-a-policy-using-the-java-api}

To create a policy by using the Java API, perform the following steps:

1. Set up your development environment and include all of the JAR files mentioned in [Setting up the development environment](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) within your project. 
1. Create a `com.adobe.flashaccess.sdk.policy.Policy` object and specify its properties, such as the rights, license caching duration, and policy end date. 

   ```java
     // Create a new Policy object.  
     // False indicates the policy does not use license chaining.  
     Policy policy = new Policy(false);  
       
     policy.setName("DemoPolicy");  
       
     // Specify that the policy requires authentication to obtain a license.  
     policy.setLicenseServerInfo  
      (new LicenseServerInfo(AuthenticationType.UsernamePassword));  
       
     // A policy must have at least one Right, typically the play right  
     PlayRight play = new PlayRight();  
       
     // Users may only view content for 24 hours.  
     play.setPlaybackWindow(24L * 60 * 60);  
       
     // Add the play right to the policy.  
     List<Right> rightsList = new ArrayList<Right>();  
     rightsList.add(play);  
     policy.setRights(rightsList);  
       
     // Licenses may be stored on the client for 7 days after downloading  
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

1. Serialize the `Policy` object and store it in a file or database. 

   ```java
     // Serialize the policy  
     byte[] policyBytes = policy.getBytes();  
     System.out.println("Created policy with ID: " + policy.getId());  
        
     // Write the policy to a file.   
     // Alternatively, the policy may be stored in a database.  
     FileOutputStream out = new FileOutputStream("demopolicy.pol");  
     out.write(policyBytes);  
     out.close();
   ```

For the full source of this sample code, see *com.adobe.flashaccess.samples.policy.CreatePolicy* in the Reference Implementation Command Line Tools “ [!DNL samples]” directory.
