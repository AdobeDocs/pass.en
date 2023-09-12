---
title: Updating a policy using the Java API
description: Updating a policy using the Java API
copied-description: yes
exl-id: 1b03f033-0d29-46cc-ae14-d6fef96fe970
---
# Updating a policy using the Java API {#updating-a-policy-using-the-java-api}

To update a policy by using the Java API, perform the following steps:

1. Set up your development environment and include all of the JAR files mentioned in [Setting up the development environment](../../aaxs-protecting-content/content-setting-up-the-sdk/content-setting-up-the-dev-env.md) within your project. 
1. Create a `Policy` instance and read in the policy from a file or database. 

   ```
   Policy policy = new Policy(policyBytes);
   ```

1. Update the `Policy` object by setting its properties, such as its name and usage rules. 

   ```java
     // Change the policy name.  
     policy.setName("UpdatedDemoPolicy");  
       
     // Add DRM module restrictions to the play right  
     for (Right r: policy.getRights()) {  
      if (r instanceof PlayRight) {  
       PlayRight pr = (PlayRight) r;  
       // Disallow Linux versions up to and including 1.9.  Allow  
       // all other OSes and Linux versions above 1.9  
       VersionInfo toExclude = new VersionInfo();  
       toExclude.setOS("Linux");  
       toExclude.setReleaseVersion("1.9");  
       Collection<VersionInfo> exclusions = new ArrayList<VersionInfo>();  
       exclusions.add(toExclude);  
       ModuleRequirements drmRestrictions = new ModuleRequirements();  
       drmRestrictions.setExcludedVersions(exclusions);  
       pr.setDRMModuleRequirements(drmRestrictions);  
       break;  
      }  
     }
   ```

1. Serialize the updated `Policy` object and store it in a file or database. 

   ```java
      // Serialize the policy.  
      byte[] policyBytes = policy.getBytes();  
      System.out.println("New policy revision number: "  
       +  policy.getRevision());      
      // Write the policy to a file.   
      // Alternatively, the policy may be stored in a database.  
      FileOutputStream out = new FileOutputStream("demopolicy-updated.pol");  
      out.write(policyBytes);  
      out.close(); 
   ```

For the full source of this sample code, see `com.adobe.flashaccess.samples.policy.UpdatePolicy` in the Reference Implementation Command Line Tools "samples" directory.
