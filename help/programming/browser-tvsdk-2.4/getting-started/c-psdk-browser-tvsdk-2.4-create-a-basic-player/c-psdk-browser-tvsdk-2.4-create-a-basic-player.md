---
description: To use Browser TVSDK, you must create and configure a basic player. For playing video content, you can create a basic player in either of two ways  using the Browser TVSDK, or using the UI Framework.
title: Basic player
exl-id: f51d7bf7-1784-447e-97ab-275ea53d5e46
---
# Overview {#basic-player-overview}

To use Browser TVSDK, you must create and configure a basic player. For playing video content, you can create a basic player in either of two ways: using the Browser TVSDK, or using the UI Framework.

## Using the Browser TVSDK {#section_4D1C6D4B3A3447DFA2AA0229E140E2D9}

Use the APIs provided with the Browser TVSDK directly to code your video player. The SDK provides you with frameworks and utilities, as well as a reference player to work from. 

>[!TIP]
>
>To see this working in a reference player, do not specify any attributes with `videoDiv`.

## Using the UI framework {#section_AE02384CFEF64A448C108232AB62A9FF}

This module is used to create instances of the player, where each instance is bound to a document object model (DOM) element that is provided by the caller. In addition to having an instance of the Browser TVSDK, each player instance hosts a number of controls that make up the user interface for the player.

The implementation of each control consist of two aspects:

* An `HTMLElement`, which is the visual representation of the component on the screen 
* A `Behavior`, which manages the `HTMLElement` and provides an API for interactions

The details about these controls are provided to the `VideoPlayer` by using a config object, which is passed to the player at its instantiation. By default, each component forms a hierarchy of objects, with the element being provided to the player instance at the root of the tree. As each component is created, it is added to the DOM at the appropriate location.

Each component has a name, which is its key in the config object when the object is registered. The CSS class of the underlying DOM element is formed as a `vp-` prefix that is added to the component name.

Components might be extended or replaced, their configuration can be altered, and initial properties set. This allows you to have broader control over API properties, the CSS class name and, optionally, aspects of the component implementation. These options can be used to customize functionality and allow multiple instances of a component that can be styled or individually configured.

All component instances can be accessed with the `.behaviors` property. Instances can be enabled and disabled and shown or hidden. But once the instances are created, these instances cannot be removed.
