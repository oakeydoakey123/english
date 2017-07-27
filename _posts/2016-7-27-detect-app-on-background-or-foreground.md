---
layout: blog_post
title:  "How to detect when app moves to background or foreground"
date: '2016-7-27'

tags:
    - Programming
    - Swift
    - Swift 3
    - AppLifecycle

categories:
    - Apple
    - iOS
    - Swift

author: Sadra
---

As you know, there is a lifecycle for each application:

![iOS Application Lifecycle]({{ site.url }}/assets/img/post/2016-7-27/foregroundvsbackground-0.png)

but these methods didn't help you when your app moves to background or foreground!

But as the guides in [docs](https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/StrategiesforHandlingAppStateTransitions/StrategiesforHandlingAppStateTransitions.html) there is more information about application lifecycle.

When you app goes to background, the core broadcast a notification app moves to background. So, if your app or your ViewController registered for this notification, you can be aware when your app moves to background:

![iOS Application Moves to Background]({{ site.url }}/assets/img/post/2016-7-27/foregroundvsbackground-2.png)

As the same, for Moving to Foreground, we have notification:

![iOS Application Moves to Foreground]({{ site.url }}/assets/img/post/2016-7-27/foregroundvsbackground-1.png)

So, you have to ways to detect when your app moves to background ofr foreground:

### In AppDelegate

That implemented by default in app delegation, and you can use this default methods for the issue:

```swift
func applicationDidEnterBackground(_ application: UIApplication) {
    // Use this method to release shared resources, save user data, invalidate timers, and store enough application state information to restore your application to its current state in case it is terminated later.
    // If your application supports background execution, this method is called instead of applicationWillTerminate: when the user quits.
    print("applicationDidEnterBackground")

}

func applicationWillEnterForeground(_ application: UIApplication) {
    // Called as part of the transition from the background to the active state; here you can undo many of the changes made on entering the background.
    print("applicationWillEnterForeground")
}
```

### In UIViewController

If you want detect it in a UIViewController manually, you should register for the `UIApplicationWillEnterForeground` or `UIApplicationDidEnterBackground` notification anywhere in your app. That it's triggered when user pressed home button and it moves to background, and then pressed double and choose app so it moves to foreground.

- ForeGround

```swift
let notificationCenter = NotificationCenter.default
notificationCenter.addObserver(self, selector: #selector(appMovedToBackground), name: Notification.Name.UIApplicationWillEnterForeground, object: nil)

func appMovedToForeground() {
    print("App moved to ForeGround!")
}
```

- Background

```swift
let notificationCenter = NotificationCenter.default
notificationCenter.addObserver(self, selector: #selector(appMovedToBackground), name: Notification.Name.UIApplicationDidEnterBackground, object: nil)

func appMovedToBackground() {
    print("App moved to Background!")
}
```

### Did this solution work for you? Please pass it on!
[Tweet](https://twitter.com/share)