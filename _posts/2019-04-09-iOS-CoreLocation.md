---
layout: post
title: iOS - Core Location
subtitle: Basics
show-avatar: false
---

# iOS -Core Location
Core Location provides services for determining a device’s geographic location, altitude, orientation, or position relative to a nearby iBeacon. The framework uses all available onboard hardware, including Wi-Fi, GPS, Bluetooth, magnetometer, barometer, and cellular hardware to gather data.

The first time that your app requests authorization, its authorization status is indeterminate and the system prompts the user to grant or deny the request (as shown in  [Figure 1](https://developer.apple.com/documentation/corelocation#2926825)). The system records the user's response and does not display this panel upon subsequent requests.

## Steps

 1. Request Permission(also configure capabilities and info.plist)
 -  **When-in-use authorization.** Your app can use most services but cannot use services that automatically relaunch the app. Your app must always start services while running in the foreground. If you enable the background location capability for your app, a suspended app will wake in the background to handle location events. However, if your app is not running, it will not be launched.
    
-   **Always** **authorization.**  Your app can use all location services, and it can start those services from either the foreground or the background. If a location-related event occurs when your app is not running, the system launches your app and delivers the event.


 2. determining whether services are available
 
 4.  start  services using the  [`CLLocationManager`](https://developer.apple.com/documentation/corelocation/cllocationmanager)  object 
 5.  receive the results in your associated delegate object.

## Services available

 - **Standard location service**
	 A configurable, general-purpose solution for getting the user's location in real time. This service uses significantly more power than the other location services, but it delivers the most accurate and immediate location information.

	Use this service only when you really need it, such as when offering navigation instructions or when recording a user's path on a hike.This service requires either In-Use or Always authorization.

- **Significant-change location service**
	  A power-friendly alternative for apps that need to track the user's location but do not need frequent updates or the precision offered by GPS. This service relies on lower-power alternatives to determine the user's location and delivers updates only when significant changes to that location occur.
	You might use this service to deliver suggestions for nearby points of interest when the user is walking.This service requires Always authorization.
 - **Visits service**
	 The most power-efficient way to gather location data. This service delivers location updates when the user has spent time in one location and then moves on. Each update includes both the location and the amount of time spent at that location.

	This service is not intended for navigation or other real-time activities. Instead, use it to identify patterns in the user's behavior and apply that knowledge to other parts of your app. For example, a music app might prepare a workout playlist when the user leaves the house and heads to the gym.This service requires Always authorization.
	
 - **Region monitoring**
	 Region monitoring (also known as geofencing) is a way for your app to be alerted when the user enters or exits a geographical region. You might use region monitoring to perform location-related tasks. For example, the Reminders app uses them to trigger reminders when the user arrives at or leaves a specified location
	In iOS, regions are monitored by the system, which wakes up your app as needed when the user crosses a defined region boundary. In macOS, region monitoring works only while the app is running (either in the foreground or background) and the user’s system is awake. The system does not launch Mac apps to deliver region-related notifications
 - **iBeacon ranging**
	 An iBeacon is a device that emits a Bluetooth signal that can be detected by your devices. Companies can deploy iBeacon devices in environments where proximity detection is a benefit to users, and apps can use the proximity of beacons to determine an appropriate course of action. You decide what actions to take based on the proximity of nearby beacons. For example, a department store might deploy beacons identifying each section of the store, and the corresponding app might point out sale items when the user is near each section.

	Adding iBeacon support to your app involves detecting beacons in two different stages:

	1.  Use region monitoring to detect the presence of an iBeacon.
    
	2.  Use beacon ranging to determine the proximity to a detected iBeacon.
    

	Using a two-step process for detecting beacons significantly reduces power consumption. Ranging requires taking frequent measurements of the strength of Bluetooth signals and computing the distance to the associated beacons. By contrast, region monitoring involves only passive listening for nearby beacons, which consumes far less power.
	
 - **Heading service**
	 Heading and course information are commonly used by navigation apps to help guide the user to a destination. The heading of a user's device is its current orientation relative to magnetic or true north. Devices with GPS can report course information, which represents the direction in which the device is moving. The Compass app in iOS uses heading information to implement a magnetic compass interface.Augmented reality apps might use this information to determine which direction the user is facing.
 - **Geocoding services**
	 The  [`CLLocationManager`](https://developer.apple.com/documentation/corelocation/cllocationmanager)  object reports locations as a latitude/longitude pair. While these values uniquely represent any location on the planet, they are not values that users immediately associate with the location. Users are more familiar with names that describe a location, such as street names or city names. The  [`CLGeocoder`](https://developer.apple.com/documentation/corelocation/clgeocoder)  class lets you convert between geographic coordinates and the user-friendly names associated with that location. You can convert from either a latitude/longitude pair to a user friendly place name(**reverse geocoding)**, or the other way around.

## Configuring Standard Location Services

 -  **distanceFilter**
	 The minimum distance (measured in meters) a device must move horizontally before an update event is generated.To minimize power consumption, never set the [`desiredAccuracy`](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423836-desiredaccuracy) property to a higher accuracy than what you actually need
 - **desiredAccuracy**
	 The accuracy of the location data.The receiver does its best to achieve the requested accuracy; however, the actual accuracy is not guaranteed.Always set the [`distanceFilter`](https://developer.apple.com/documentation/corelocation/cllocationmanager/1423500-distancefilter) property to the greatest value that meets the needs of your app.
- **pausesLocationUpdatesAutomatically**
A Boolean value indicating whether the location manager object may pause location updates.Allowing the location manager to pause updates can improve battery life on the target device without sacrificing location data.After a pause occurs, it is your responsibility to restart location services again when you determine that they are needed.
-  **activityType**
	The type of user activity associated with the location updates. Location manager uses the information in this property as a cue to determine when location updates may be automatically paused.
- **allowsBackgroundLocationUpdates**
A Boolean value indicating whether the app should receive location updates when suspended.When the value of this property is  `false`, apps receive location updates normally while running in either the foreground or background based on its current authorization. Updates stop only when the app is suspended, thereby preventing the app from being woken up to handle those events.
- **showsBackgroundLocationIndicator**
	A Boolean indicating whether the status bar changes its appearance when location services are used in the background.This property affects only apps that received always authorization. When such an app moves to the background, the system uses this property to determine whether to change the status bar appearance to indicate that location services are in use. Displaying a modified status bar gives the user a quick way to return to your app.

## Handling Location Events in the Background
ost location services are meant to be used while your app is in the foreground, but some can also run in the background or even cause your app to be launched. To receive events in the background, configure the Location updates capability for your app in Xcode. You must also set the [`allowsBackgroundLocationUpdates`](https://developer.apple.com/documentation/corelocation/cllocationmanager/1620568-allowsbackgroundlocationupdates) property of your `CLLocationManager` object to `true`.

When the system launches your app, use the launch options dictionary passed to the [`application(_:willFinishLaunchingWithOptions:)`](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1623032-application) and [`application(_:didFinishLaunchingWithOptions:)`](https://developer.apple.com/documentation/uikit/uiapplicationdelegate/1622921-application) methods to determine whether your app was launched to handle a location update. This dictionary contains the [`location`](https://developer.apple.com/documentation/uikit/uiapplication/launchoptionskey/1623101-location) key when the app is launched because of location services. Create a new [`CLLocationManager`](https://developer.apple.com/documentation/corelocation/cllocationmanager) object, configure it with a delegate, and start location services again to receive the update.

> *Significant-change location service,Visits service,Region monitoring* can relaunch your app after it has been terminated.


	

