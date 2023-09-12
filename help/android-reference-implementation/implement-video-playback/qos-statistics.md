---
description: You can set up your player to read playback and device statistics from the QoSProvider as often as needed.
title: Display QoS playback and device statistics
exl-id: 369b6e9a-70a2-4f62-a1bf-f69030c5d6c3
---
# Display QoS playback and device statistics {#display-qos-playback-and-device-statistics}

You can set up your player to read playback and device statistics from the QoSProvider as often as needed.

The `QoSProvider` class provides various statistics, including the frame rate, the profile bit rate, the total time spent in buffering, the number of buffering attempts, the time it took to get the first byte from the first video fragment, the time it took to render the first frame, the currently buffered length, and the buffer time.

The reference implementation provides a `QoSManager` class where you can enable the display of the QoS overlay. You can also enable the QoS visibility in the Settings user interface:

![](assets/qos-configuration.jpg)

The `QoSManager` tracks QoS statistics by getting device information, attaching to the media player, and updating with the latest QoS information.

**Enable or disable QoS statistics reporting**

1. Create a QosManager or enable QoS reporting using the ManagerFactory.

   * To create a QosManager:
        * This application needs to use the advertising workflow feature 
   
   QoSManager qosManager = new QosManagerOn();

    * To use a ManagerFactory to enable the display of QoS statistics:

    qosManager = ManagerFactory.getQosManager( 
    <b>true</b>, config, mediaPlayer);

    >[!NOTE]
    >
    >Changing the boolean to `false` disables QoS reporting.

2. Add event listeners:

   `qosManager.addEventListener(qosManagerEventListener);`

3. Create the QoS provider and attach it to the player activity context:

   `qosManager.createQOSProvider(getActivity());`

   >[!NOTE]
   >
   >When the player activity is going to be destroyed, make sure to call [qosManager.destroyQOSProvider](https://help.adobe.com/en_US/primetime/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html#destroyQOSProvider()) to clean up the QOS provider by detaching it from the media player.

**Related API documentation**
   
* [Class QosManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.html)
* [Class QosManagerOn](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManagerOn.html)
* [QosManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosManagerEventListener.html)
* [QosItem](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/QosManager.QosItem.html)
