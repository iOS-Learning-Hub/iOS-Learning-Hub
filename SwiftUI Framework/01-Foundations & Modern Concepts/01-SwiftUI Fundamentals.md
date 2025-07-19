# SwiftUI Fundamentals

## Introduction: Why SwiftUI is different?

SwiftUI is a modern way to declare user interfaces for any Apple platform. The key insight is that SwiftUI is **declarative** rather than **imperative**. You describe *what* the UI should look like for any given state, not *how* to change it.

---

## The Declarative Paradigm

### UIKit (Imperative)

```
import UIKit

// UIKit - You tell the system *HOW* to change
let button = UIButton()
button.setTitle("Click me", for: .normal)
button.backgroundColor = UIColor.blue

// Later, when state changes:

if isEnabled {
    button.setTitle("Enabled", for: .normal)
    button.backgroundColor = UIColor.blue
} else {
    button.setTitle("Disabled", for: .normal)
    button.backgroundColor = UIColor.gray
}
```

### SwiftUI (Declarative)

```
import SwiftUI

struct MyButton: View {
    var isEnabled: Bool

    var body: some View {
        Button(isEnabled ? "Enabled" : "Disabled") {
            // Action
        }
        .foregroundColor(.white)
        .background(isEnabled ? .blue : .gray)
    }
}
```
---

## Framework Comparison

Understanding SwiftUI is easier when you relate it to what you already know:

| Concept | SwiftUI | React Native | Flutter | Android Compose|
| ---- | ---- | ---- | ---- | ---- |
|  **Basic Unit** | View (struct) | Component (function/class) | Widget (class) | Composable (function) |
| **State Updates** | Automatic on state change | setState() or hooks | setState() | Recomposition |
| **Layout** | VStack, HStack, ZStack | Flexbox (View) | Column, Row, Stack | Column, Row, Box |
| **Styling** | Modifiers | Style objects | Widget properties | Modifier chains |

---

## Basic SwiftUI Structure

### App Entry Point

To indicate your app entry point, you precede the structure's definition with the *@main* attribute to indicate that your custom App protocol conformer provides the entry point into your app. You can have exactly one entry point among all of your app's files.

```
import SwiftUI

@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView() // Your root view
        }
    }
}
```


### Views and the View Protocol

Views are building blocks that you use to declare your app's user interface. Each view contains a description of what to display for a given state. Every bit of your app that's visible to the user derives from the description in a view, and any type that conforms to the **View** protocol can act as a view in your app.

You create custom views by declaring types that conform to the **View** protocol. Implement the required <ins>body</ins> computed property to provide the content for your custom view

```
import SwiftUI

struct ContentView: View {
    var body: some View {
        Text("Hello, World!")
    }
}
```

**Key points:**
- Views are **structs**, not classes (value types, lightweight)
- `body` is a required computed property that returns another view
- `some View` means "some type that conforms to View protocol, but we don't want to say what". It means even though we don't know what view type is going back, the compiler does.
- Views describe what should appear, not how to build it



### Core UI Elements

#### Text
A text view draws a string in your app's user interface using a <ins>[body](https://developer.apple.com/documentation/swiftui/font/body)</ins> font that's appropriate for the current platform. You can choose a different standard font, like <ins>[title](https://developer.apple.com/documentation/swiftui/font/title)</ins> or <ins>[caption](https://developer.apple.com/documentation/swiftui/font/caption)</ins>, using the <ins>[font(_: )](https://developer.apple.com/documentation/swiftui/view/font(_:))</ins> view modifier.

```
import SwiftUI

struct TextExamples: View {
    var body: some View {
        VStack(spacing: 16) {
            // Basic text
            Text("Hello, world!")

            // Styled text
            Text("Large Title")
                .font(.largeTitle)
                .fontWeight(.bold)
                .foregroundColor(.blue)
            
            // Multi-line text
            Text("This is a longer text that will wrap across multiple lines when needed.")
                .multilineTextAlignment(.center)
                .lineLimit(3)

            // Rich text with markdown (iOS 15+)
            Text("You can make text **bold** and *italic*")
        }
        .padding()
    }
}
```
#### Button
You create a button by providing and action and a label. The action is either a method or closure property that does something when a user clicks or taps the button. The label is a view that describes the button's action.

The label of a button can be any kind of view, such as <ins>[Text](https://developer.apple.com/documentation/swiftui/text)</ins> view for text-only labels:

```
Button(actions: signIn) {
    Text("Sign In")
}
```

Or a <ins>[Label](https://developer.apple.com/documentation/swiftui/label)</ins> view, for buttons with both a title and an icon:

```
Button(action: signIn) {
    Label("Sign In", systemImage: "arrow.up")
}
```

Example using different button styles:
```
struct ButtonExamples: View {
    @State private var tapCount = 0
    
    var body: some View {
        VStack(spacing: 16) {
            // Simple button
            Button("Tap Me") {
                tapCount += 1
            }
            
            // Button with custom styling
            Button(action: { tapCount += 1 }) {
                Text("Custom Button")
                    .padding()
                    .background(Color.blue)
                    .foregroundColor(.white)
                    .cornerRadius(8)
            }
            
            // Button with system image
            Button(action: { tapCount += 1 }) {
                Label("Add Item", systemImage: "plus")
            }
            .buttonStyle(.borderedProminent)
            
            Text("Tapped \(tapCount) times")
                .font(.caption)
                .foregroundColor(.secondary)
        }
        .padding()
    }
}
```

#### Image
Use an Image instance when you want to add images to your SwiftUI app. You can create images from many sources:

- Image files in your app's asset library or bundle. Supported types include: PNG, JPEG, HEIC, and more.
- Instances of platform-specific image types, like <ins>[UIImage](https://developer.apple.com/documentation/UIKit/UIImage)</ins> and <ins>[NSImage](https://developer.apple.com/documentation/AppKit/NSImage)</ins>.
- A bitmap stored in a Core Graphics <ins>[CGImage](https://developer.apple.com/documentation/CoreGraphics/CGImage)</ins> instance.
- System graphics from the SF Symbols set.

The following example shows how to load an image from the app's asset library or bundle and the SF Symbols set:

```
import SwiftUI

struct ImageExample: View {
    var body: some View {
        VStack(spacing: 16) {
            // System image (SF Symbols)
            Image(systemName: "heart.fill")
                .font(.largeTitle)
                .foregroundColor(.red)

            // Bundle image
            Image("Landscape_4")
                .resizable()
                .aspectRatio(contentMode: .fit)
                .frame(width: 200, height: 200)
        }
    }
}
```
#### Layout Containers

##### VStack, HStack, ZStack



##### Alignment and Spacing

##### View Modifiers

---

## 🛫 Next Steps

Now that you understand the fundamentals of SwiftUI, you're ready to dive deeper into how the view system works and how to manage state effectively.

#### What You've Learned
- ✅ **Declarative vs Imperative**: How SwiftUI differs from UIKit
- ✅ **Basic Views**: Text, Button, Image, and their modifiers
- ✅ **Layout**: VStack, HStack, ZStack, and alignment
- ✅ **User input**: Forms, validation and basic @State
- ✅ **Navigation**: Moving between screens
- ✅ **Lists**: Displaying and managing collections of data

#### Where to Go Next

**Continue to** [Views & View Hierarchy](/SwiftUI/Foundations%20&%20Modern%20Concepts/Views%20&%20View%20Hierarchy.md)
-   Understand how SwiftUI's view system works under the hood
-   Learn about view identity, lifecycle, and performance
-   Master view composition and custom components
-   

**Or jump to specific topics:**
- Need state management? -> [State Management Basics]()
- Ready for data flow? -> [Advanced State & Data Flow]()
- Want to save data? -> [Data Persistence with SwiftData]()

---

## 📚 Resources

- [Imperative UI programming vs Declarative UI programming](https://medium.com/@saiful103a/imperative-ui-programming-vs-declarative-ui-programming-c4000d9fe835)
- [App | Apple Developer Documentation](https://developer.apple.com/documentation/swiftui/app)
- [View | Apple Developer Documentation](https://developer.apple.com/documentation/swiftui/view)
- [Why does SwiftUI use "some View" for its View type?](https://www.hackingwithswift.com/books/ios-swiftui/why-does-swiftui-use-some-view-for-its-view-type)
- [Button | Apple Developer Documentation](https://developer.apple.com/documentation/swiftui/button)
- [Text | Apple Developer Documentation](https://developer.apple.com/documentation/swiftui/text)
- [Image | Apple Developer Documentation](https://developer.apple.com/documentation/swiftui/image)
- [Buttons and Images](https://www.hackingwithswift.com/books/ios-swiftui/buttons-and-images)