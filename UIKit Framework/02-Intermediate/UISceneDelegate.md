###### Protocol
# UISceneDelegate


## What is it?
The core methods you use to respond to life-cycle events occurring within a scene.

- Use your UISceneDelegate object to manage life-cycle events in one instance of your app's user interface.
- This interface defines methods for responding to state transitions that affect the scene, including when the scene enters the foreground and becomes active, and when it enters the background.
- Use your delegate to provide appropriate behavior when these transitions occur. For example, finish critical tasks and quiet your app when it enters the background.
- **Don't create UISceneDelegate objects directly.** Instead, specify the name of your custom delegate class as part of the configuration data for your scenes. You can specify this information in your app's `Info.plist` file, or in the UISceneConfiguration object you return from your app delegate's application(_:configurationForConnecting:options:) method. For more information about how to configure scenes, see [Specifying the scenes your app supports](https://developer.apple.com/documentation/uikit/specifying-the-scenes-your-app-supports)

---

## 



## 📚 Resources

- [UISceneDelegate | Apple Developer Documentation](https://developer.apple.com/documentation/uikit/uiscenedelegate)
- [Defining custom scenes in SwiftUI](https://nilcoalescing.com/blog/CustomScenesInSwiftUI/#:~:text=Scenes%20are%20a%20core%20concept,organizing%20and%20maintaining%20complex%20applications.)

## 🔙 Topics
- [Go back to README](/UIKit%20Framework/README.md)