# Comments and Documentation

## 🎯 Learning Objectives

By the end of this lesson you will:
- Understand the different types of comments in Swift and when to use each
- Learn best practices for writing clear and meaningful comments in your code
- Master Xcode's documentation features for accessing Apple's official documentation
- Create your own documentation using Swift's documentation comments
- Use Xcode shortcuts and tools to efficiently browse and generate documentation
- Understand the importance of self-documenting code and proper documentation practices

---

## ✍️ Comments

Use comments to include nonexecutable text in your code, as a note or reminder to yourself. Comments are ignored by the Swift compiler when your code is compiled

**Single-line comments** begin with two forward-slashes (//)

**Multiline comments** start with a forward-slash followed by an asterisk ( /* ) and end with an asterisk followed by a forward-slash (*/)

```

// This is a comment


/* This is also a comment
but is written over multiple lines. */

/* This is the start of the first multiline comment.
    /* This is the second, nested multiline comment. */
This is the end of the first multiline comment. */

```
---

## Documentation

You can access documentation for methods and symbols or create your own documentation in Xcode by following these instructions:
- **Option + Click**: Hold down the Option key and click on the method, class, or symbol you want to view documentation for. This will display a Quick Help popover with relevant information, including a link to open the full documentation in the Developer Documentation window.
- **Command + Shift + 0**: This shortcut directly opens the Developer Documentation window, allowing you to browse or search for specific documentation.
- **Quick Help Inspector**: Ensure the Quick Help Inspector (the panel with the question mark icon) is open in the Utilities area (right-hand side panel). When you select a symbol in your code, its documentation will automatically appear in this inspector.
- **Editor > Add Documentation**: Place your cursor before a method or class definition and press Command + Option + /. Xcode will automatically generate a documentation block (///) for you to fill in. This is for documenting your own code (classes, methods, functions, etc).

### Best Practices for Comments and Documentation

- **Write clear, concise comments** that explain the "why" rather than the "what"
- **Keep comments up to date** when you modify your code
- **Use documentation comments** for public APIs and complex functions
- **Avoid obvious comments **that simply restate what the code does
- **Use consistent formatting** and style throughout your codebase
---

## 🛫 Next Steps

#### What You've Learned
- ✅ **Single-line Comments**: Using // for brief notes and reminders in your code
- ✅ **Multiline Comments**: Using /* */ for longer explanations and nested comments
- ✅ **Documentation Comments**: Creating structured documentation with /// and /** */ syntax
- ✅ **Xcode Documentation Access**: Using Option+Click and keyboard shortcuts to access Apple's documentation
- ✅ **Quick Help Tools**: Leveraging Xcode's built-in documentation inspector and generation features
- ✅ **Documentation Best Practices**: Writing meaningful comments that enhance code readability and maintainability


#### Where to Go Next

**Continue to** [Collection Types](/Swift%20Fundamentals/Beginner/02-Collection%20Types/01-Collection%20Types.md)

--- 

## 📚 Resources
- [The Swift Programming Language - Comments](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Comments)
- [Xcode Help - Quick Help](https://help.apple.com/xcode/mac/current/#/dev91ef7c538)
- [Xcode - Documenting apps, frameworks, and packages](https://developer.apple.com/documentation/Xcode/documenting-apps-frameworks-and-packages)