---
description: Your application must use the appropriate PTTimedMetadata objects at the appropriate times.
title: Store timed metadata objects as they are dispatched
exl-id: 8b859e8d-eb4c-48f9-a95e-1bcc35a2a520
---
# Store timed metadata objects as they are dispatched {#store-timed-metadata-objects-as-they-are-dispatched}

Your application must use the appropriate PTTimedMetadata objects at the appropriate times.

 During content parsing, which happens before playback, TVSDK identifies subscribed tags and notifies your application about these tags. The time that is associated with each `PTTimedMetadata` is the absolute time on the playback timeline.

Your application must complete the following tasks: 

1. Keep track of the current playback time.
1. Match the current playback time to the dispatched `PTTimedMetadata` objects.

1. Use the `PTTimedMetadata` where the start time equals the current playback time.

   >[!NOTE]
   >
   >The code below assumes that there is only one `PTTimedMetadata` instance at a time. If there are multiple instances, the application must save them appropriately in a dictionary. One method is to create an array at a given time and store all instances in that array.

   The following example shows how to save `PTTimedMetadata` objects in a `NSMutableDictionary (timedMetadataCollection)` keyed by the start time of each `timedMetadata`. 

   ```
   NSMutableDictionary *timedMetadataCollection; 
     
   - (void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
   { 
       if (!timedMetadataCollection) 
       { 
           timedMetadataCollection = [[NSMutableDictionary alloc] init]; 
       } 
       NSDictionary *userInfo = [notification userInfo]; 
       PTTimedMetadata *timedMetadata = [(PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey] retain]; 
       if ([timedMetadata.name  isEqualToString: @"#EXT-OATCLS-SCTE35"]) 
       { 
            NSLog(@"Adding timedMetadata %@ to timedMetadataCollection with time                      
                    %f",timedMetadata.name,CMTimeGetSeconds(timedMetadata.time)); 
     
           NSNumber *timedMetadataStartTime = [NSNumber numberWithInt:(int)CMTimeGetSeconds(timedMetadata.time)]; 
           [timedMetadataCollection setObject:timedMetadata forKey:timedMetadataStartTime]; 
       } 
       [timedMetadata release]; 
   }
   ```

## Parsing Nielsen ID3 tags {#example_3B51E9D4AF2449FAA8E804206F873ECF}

To extract the ID3 tag for parsing, use the following on the `onMediaPlayerSubscribedTagIdentified` method: 

```
(void)onMediaPlayerSubscribedTagIdentified:(NSNotification *)notification 
{ 
NSDictionary *userInfo = [notification userInfo]; 
PTTimedMetadata *timedMetadata = (PTTimedMetadata *)[userInfo objectForKey:PTTimedMetadataKey]; 
if (timedMetadata.type == PTTimedMetadataTypeID3) 
Unknown macro: { PTMetadata *metadata = (PTMetadata *)timedMetadata; NSString * nstr = [[NSString alloc] initWithFormat} 
 
}
```

After you parse the ID3 tag, extract the Nielsen-specific metadata using the following: 

```
    (NSString *)parseNielsenUrlFromID3Tag:(NSString *)str 
    { 
    /* ID3 tag <AVMetadataItem: 0x15e58e60, identifier=id3/PRIV, keySpace=org.id3, key class = __NSCFString, key=PRIV, commonKey=(null), extendedLanguageTag=(null), dataType=(null), time= {110265598/4410000 = 25.004} 
 
    , duration= 
    {INVALID} 
 
    , startDate=(null), extras= 
    { info = "www.nielsen.com/X100zdCIGeIlgZnkYj6UvQ==/pI-X5FFk07770SXf2ZbI6g==/CE0C6​1TsDo0jIrNn9N2yTPe6nVG3dHZHfgS52fJeQjf9fJCga9tj4OW4NXPZ9fI1mx0gfYUPBXnjqolHemZPtn_FCoNg​8Dqw8-Auruf15fU04pJfXTTN0IgZ4iWBmeRiPpS9X100zdCIGeIlgZnkYj6UvVjmPIdY5jyRQTA=/00000/21778/00"; } 
 
    , value length=1> 
    */ 
 
NSString *nielsenStr = nil; 
for (NSString *keyValuePairString in [str componentsSeparatedByString:@", "]) 
{ 
if([keyValuePairString rangeOfString:@"nielsen.com"].location != NSNotFound) 
{ // Nielsen NSRange start = [keyValuePairString rangeOfString:@"\""]; NSRange end = [keyValuePairString rangeOfString:@"\";"]; nielsenStr = [keyValuePairString substringWithRange:NSMakeRange(start.location + 1, end.location-start.location)]; } 
 
} 
return nielsenStr; 
}
```
