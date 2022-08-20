---
title: "Introduction to Android Development"
subtitle: "The Android System Architecture"
author:
    name: "Alvin Fungai"
layout: post
---

When I first came to Android development a couple of years ago having just come from learning the Java language, I discovered there were new terms that just were hard to grasp. I ran into terms like `context`, `lifecycle`, `memory leaks` among several others. The definitions in the [developer documentation](https://developer.android.com/reference/android/content/Context) were not very helpful at the time. 


In this post I will atempt to provide simplified explanations of these important terms in the best way I can so that I wish I had when I first started. We shall start with the `activity`, `application`, `fragment`, followed by `context` then `lifecycle` and finally address `memory leaks` in relations with the previous terms.

## Activity
An `activity` is defined as a single screen that is currently displayed on the device. The activity exposes a set of related features representing part of the `application` as an interactive UI interface.

## Fragment
A `fragment` is a class that is closely associated with and managed by an activity to implement UI components to compose a screen.

## Application
An `application` is a set of activities which when taken together solve a domain problem. An example of a domain problem would be a requirement to organize and manage user task at specific times. An application would then need screens for creating new tasks, listing, updating and deleting existing task. Each of those screens are then defined as classes known as activities in Android.

## Context
On an Android device, there are many processes that run concurrently in memory. There is therefore need to manage all running processes so that available are allocated efficiently. Otherwise, the device will become unresponsive or even running apps may crash leading to bad user experience.

`Context` is an abstract class that defines an isolated environment in which each application runs. It is the base class of both application and activity classes. The context is implemented by the Android system. There are 2 types of context:

1. `Application context` which is tied to the `lifecycle` of the application. It is a singleton class that is globally accessible to all activities of a class. It remains defined even when a user navigates between screens. Shared resources such as storage, preferences, services, calling and managing activities are found at the application-level in the application context.
In the `Kotlin language` the application context which can be accessed application-wide is usually accessed using the function `getApplicationContext()`.

2. `Activity context` which is tied to the `lifecycle` of an activity. Each activity has its own context that is specific to it and only itself. Once a currently active activity is destroyed the activity context associated with it is marked for garbage collection by the Android system to free us memory and resources.
In Kotlin we access context inside an activity by the keyword `this`.


![Android context](/assets/img/ContextDiag.png){:style="display:block; margin-left:auto; margin-right:auto"}

## Lifecycle
Activities and fragments in Android have a `lifecycle` which is used to track state using event callbacks for each stage the activity or fragment is in. Lifecycle stages can be summarized as follows. See [developer documentation](https://developer.android.com/guide/components/activities/activity-lifecycle) for more details.


## Activity Lifecycle

### onCreate()
Called when the activity starts. This is where we specify the layout resource file

### onStart()
Called when the activity becomes visible on the screen

### onResume()
The activity is ready for user interaction

### onPause()
Called when the current activity is replaced by another activity after a user opens another screen

### onStop()
The activity is no longer visible on the screen

### onDestroy()
Called before activity is destroyed by the Android system to free resources and avail them to other processes

### onRestart()
Called when the a user re-opens a previous screen and resumes interacting with the activity

## Fragment Lifecycle

Fragments also have a lifecycle that is similar to that of the activity with slight differences from that of an activity. The fragment lifecycle does not specify the onResume() callback.However the fragment lifecycle specifies a few more callbacks besides the ones above:


### onCreateView()
Called after `onCreate()`. Loads the fragment and specifies the layout resource file
 
### onViewCreated()
Called after `onCreateView()`. The fragment becomes visible on the screen and is ready for user inreaction

### onDestroyView()
The fragment is detached from the activity and destroyed to free system resources.


## Memory Leaks
A `memory leak` occurs when memory allocation is not properly managed and has objects remain in heap memory after an activity is destroyed for instance. This reduces amount of memory resources and as a result slows the device down or even results in application crashes.

## Summary

This article discussed important concepts to understand before we start android development. These concepts form the basis of Android system architecture and help us as developers to write efficient code that takes advantage of interfaces that the system exposes. We defined an `application` as a set of screens to implement some business logic. An activity is simply a single screen that the user can interact with. Applications and activities can access system resources using a class called a `context` which they both extend. A fragment was defined as a UI componet the composes an activity.
Finally we discussed `lifecycle` as callbacks that are used to track state in an activity or fragment. In the next article we will start practical Android application development.
