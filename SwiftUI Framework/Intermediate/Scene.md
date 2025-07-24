###### Protocol
# Scene

## What is it?
- A part of an app's user interface with a life cycle managed by the system.
- You create an [App](https://developer.apple.com/documentation/swiftui/app) by combining one or more instances that conform to the Scene protocol in the app's body. 
```
struct MyScene: Scene {
    var body: some Scene {
        WindowGroup {
            MyRootView()
        }
    }
}
```
- A scene acts as a container for a view hierarchy that you want to display to the user. The system decides when and how to present the view hierarchy in the user interface in a way that’s platform-appropriate and dependent on the current state of the app.


## 📚 Resources
- [Scene | Apple Developer Documentation](https://developer.apple.com/documentation/swiftui/scene)
- [Defining custom Scenes in SwiftUI](https://nilcoalescing.com/blog/CustomScenesInSwiftUI/#:~:text=Scenes%20are%20a%20core%20concept,organizing%20and%20maintaining%20complex%20applications.)

## 🔙 Topics

- [Go back to the README](/SwiftUI%20Framework/README.md)