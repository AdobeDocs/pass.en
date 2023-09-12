---
description: This section covers the grammar of the configuration input, emphasizing valid and invalid input options, and explaining how omitted optional fields are interpreted.
title: RBOP Grammar
exl-id: 311194ec-e59b-4145-b22b-6983e212fcab
---
# RBOP Grammar {#rbop-grammar}

This section covers the grammar of the configuration input, emphasizing valid and invalid input options, and explaining how omitted optional fields are interpreted.

The resolution-based output protection grammar is defined as a sequence of rules, where each rule can have multiple, valid forms:

```
Rule ::=       
 
    Form 
     
AnotherRule ::=     
 
    DifferentForm 
```

## Applying the Grammar Rules {#section_A7216BD585FF4EB88737B643B36C2781}

>[!NOTE]
>
>To help improve the readability of the grammar, the following properties are not reflected within the grammar but still hold true:

1. The order of the pairs defined within the objects is not fixed; thus, any permutation of the pairs is valid. 

   For example, if we defined an object like this: 

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   then the following structure would also be considered valid: =

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

1. For each pair within an object, it is assumed that only 1 instance of that pair exists within a given instance of a given object. 

   For example, if we defined an object like this: 

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   then the following instance would be invalid, because there are two `foo` pairs within the same object: 

   ```
   { 
     "foo":<Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>,  
   } 
   ```

   Likewise, having two objects such as:

   ```
   {  
     "foo": <Foo>,  
     "bar":<Bar>,  
     "baz":<Baz>  
   }
   ```

   and: 

   ```
   {  
     "baz":<Baz>,  
     "foo":<Foo>,  
     "bar":<Bar> 
   }
   ```

   is valid, since they are independent instances of the same object. 

1. For definitions where one or more of a sequence of strings may be chosen, treat the strings like a set, in which duplicate entries are treated as a single entry. For example, `["foo", "bar", "foo", "baz"]` is equivalent to `["foo", "bar", "baz"]` 

1. For defining numbers, a space is used between the rules, (e.g., `Digit Digits`), but no such space should be used when applying the rule. 

   For example, if we express the number *one hundred twenty three* per the NonZeroInteger rule, it should be expressed as `123` rather than `1 2 3`, even though the rule contains a space between NonZeroDigit and Digits. 

1. Some of the rules allow multiple forms. In these cases, the different forms are separated by the `'|'` character. 

   For example, this rule: 

   ```
   Foo ::= "A" | "B" | "C"
   ```

   means that an instance of `Foo` can be replaced with "A", "B", or "C". This should not be confused with a form that spans multiple lines; that is a feature to make longer forms more readable. 

## The Grammar {#section_52189FD66B1A46BA9F8FDDE1D7C8E8E8}

```
PixelBasedOPConfig ::= 
      {} 
    | { "maxPixel": NonNegativeInteger } 
    | { "pixelConstraints": PixelConstraintsSeq } 
    | { "pixelConstraints": PixelConstraintsSeq, 
        "maxPixel": NonNegativeInteger } 
 
PixelConstraintsSeq ::= 
      [] 
    | [ PixelConstraints ] 
 
PixelConstraints ::= 
      PixelConstraint 
    | PixelConstraint, PixelConstraints 
 
PixelConstraint ::= 
      { "pixelCount": NonNegativeInteger } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq } 
    | { "pixelCount": NonNegativeInteger, 
        "analog": AnalogOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
        "analog": AnalogOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
         "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "analog": AnalogOutputRestriction, 
        "ota": OTAOutputRestriction } 
    | { "pixelCount": NonNegativeInteger, 
        "digital": DigitalOutputRestrictionsSeq, 
        "analog": AnalogOutputRestriction, 
        "ota": OTAOutputRestriction } 
 
DigitalOutputRestrictionsSeq ::= 
      [] 
    | [ DigitalOutputRestrictions ] 
 
DigitalRestrictions ::= 
      DigitalRestriction 
    | DigitalRestriction, DigitalRestrictions 
 
DigitalRestriction ::= 
      { "output": DigitalOutputOption } 
    | { "output": DigitalOutputOption, "hdcp": HDCP } 
 
DigitalOutputOption ::= 
      "NO_PROTECTION" 
    | "USE_IF_AVAILABLE" 
    | "REQUIRED" 
    | "NO_PLAYBACK" 
 
HDCP ::= 
    { "major": PositiveInteger, "minor": NonNegativeInteger } 
 
AnalogOutputRestriction ::= 
    { "output": AnalogOutputOption } 
 
AnalogOutputOption ::= 
      "NO_PROTECTION" 
    | "USE_IF_AVAILABLE" 
    | "USE_IF_AVAILABLE_ACP" 
    | "USE_IF_AVAILABLE_CGMSA" 
    | "REQUIRED" 
    | "REQUIRED_ACP" 
    | "REQUIRED_CGMSA" 
    | "NO_PLAYBACK" 
 
OTAOutputRestriction ::= 
    { "whitelist": OTAWhitelistSeq } 
 
OTAWhitelistSeq ::= 
      [] 
    | [ OTAWhitelist ] 
 
OTAWhitelist ::= 
      OTAConnectionType 
    | OTAConnectionType, OTAWhitelist 
 
OTAConnectionType ::= 
      "MIRACAST" 
    | "AIRPLAY" 
    | "WIDI" 
    | "DLNA" 
 
NonNegativeInteger ::= 
      Digit 
    | NonZeroDigit Digits 
 
PositiveInteger ::= 
      NonZeroDigit 
    | NonZeroDigit Digits 
 
Digits ::= 
      Digit 
    | Digit Digits 
 
Digit ::= 
      0 
    | NonZeroDigit

NonZeroDigit ::= 
      1 
    | 2 
    | 3 
    | 4 
    | 5 
    | 6 
    | 7 
    | 8 
    | 9
```

## Semantics: Legal but invalid configurations {#section_709BE240FF0041D4A1B0A0A7544E4966}

The *Sample Output Protection Configuration* topic presented a valid configuration along with its semantic meaning. The previous section in *this* topic presented the grammar rules for configurations. While the grammar helps ensure syntactic correctness, there are syntactically legal configurations that are not semantically correct (i.e., they are not logical). This section presents configurations that are *syntactically* legal, but *semantically* incorrect. Keep in mind that the examples in this section have been reduced to the minimum structure needed to illustrate the scenario under discussion.

* It is invalid to define multiple pixel constraints with the same pixel count. 

  ```
  {  
    "pixelConstraints":  
      [  
        { "pixelCount": 720 }  
      ]  
   }  
  ```

* A pixel count must not exceed the maximum pixel resolution specified. 

  ```
  { 
    "maxPixel": 720, 
    "pixelConstraints": 
      [ 
        {"pixelCount": 1080} 
      ] 
  } 
  ```
