###### Protocol
# UIApplicationDelegate

## What is it?

The app delegate is effectively the root object of your app, and it works in conjunction with UIApplication to manage some interactions with the system. Like the UIApplication object, UIKit creates your app delegate object early in your app’s launch cycle so it’s always present.

## When to use it?
Use your app delegate object to handle the following tasks:

- Initializing your app’s central data structures

- Configuring your app’s scenes

- Responding to notifications originating from outside the app, such as low-memory warnings, download completion notifications, and more

- Responding to events that target the app itself, and aren’t specific to your app’s scenes, views, or view controllers

- Registering for any required services at launch time, such as Apple Push Notification service

## Life-cycle management in iOS 12 and earlier
In iOS 12 and earlier, you use your app delegate to manage major life cycle events in your app. Specifically, you use methods of the app delegate to update the state of your app when it enters the foreground or moves to the background.

- For information on what to do when your app enters the foreground, see Preparing your UI to run in the foreground.

- For information on what to do when your app enters the background, see Preparing your UI to run in the background.

- For general information about the life cycle of your app, see Managing your app’s life cycle.

## Life-cycle management in iOS 13 and later
In iOS 13 and later, use UISceneDelegate objects to respond to life-cycle events in a scene-based app.

## Methods
### Initializing the app
#### func application(_:willFinishLaunchingWithOptions:)
- Tells the delegate that the launch process has begun.
- Use this method (and the corresponding **application(_:didFinishLaunchingWithOptions:)** method) to initialize our app and prepare it to run.
- In an app that doesn't support scenes, the system calls this method after your app launches and loads its main storyboard or nib file, but before restoring your app's state.
- When the system calls this method, your app is in the inactive state.

#### func application(_:didFinishLaunchingWithOptions:)
- Tells the delegate that the launch process is almost done and the app is almost ready to run.
- Use this method (and the corresponding **application(_:willFinishLaunchingWithOptions:)** method) to complete your app's initialization. 
  
- In an app that support scenes:
  - The system calls this method as soon as the process is done launching
  - The system then creates the scene(s) that you configured for your app
  - The system calls scene-life-cycle methods, such as **scene(_:willConnectTo:options:)**
  - As the system presents a scene, it updates that scene's **activationState.** The app's state is the aggregate of all the scene **UIScene.ActivationState** values.
  
- In an app that doesn't support scenes:
  - The system performs state restoration before calling this method.
  - The system calls this method when the process is done launching.
  - The system presents your app’s window, scene(s), and other UI.
  - At some point after this method returns, the system calls another of your app delegate’s methods to move the app to the active (foreground) state or the background state.

### Configuring and discarding scenes

#### func application(_:configurationForConnecting:options:)
- Retrieves the configuration data for UIKit to use when creating a new scene
 

#### func application(_:didDiscardSceneSessions:)
- Tells the delegate that the user closed one or more of the app's scenes from the app switcher.
- When the user removes a scene from the app switcher, UIKit calls this method before discarding the scene’s associated session object altogether. (UIKit also calls this method to discard scenes that it can no longer display.) If your app isn’t running, UIKit calls this method the next time your app launches.
- Use this method to update your app’s data structures and to release any resources associated with the scene.
- UIKit calls this method only when dismissing scenes permanently. It doesn’t call it when the system disconnects a scene to free up memory. Memory reclamation deletes the scene objects, but preserves the sessions associated with those scenes.

### Responding to app life-cycle events

#### func applicationDidEnterBackground(_ : )


#### applicationWillTerminate\(_\:)

## 📚 Resources
- [UIApplicationDelegate | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uiapplicationdelegate)
- [iOS Application Scene Delegate vs App Delegate](https://medium.com/@Ariobarxan/ios-application-scene-delegate-vs-app-delegate-a-talk-about-life-cycle-a2ecae9d507e)

## 🔙 Topics
- [Go back to README](/UIKit%20Framework/README.md)