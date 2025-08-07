# Comments and Documentation

## 🎯 Learning Objectives

By the end of this lesson you will:
- Understand the types of comments and how to use them in your code.
- 

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

---

## 🛫 Next Steps

#### What You've Learned
- ✅ **Comments:** Use them as reminders or notes in your code.
- ✅ **Documentation:** Learn how to quickly access the documentation from Apple for classes/methods or create your own documentation for your code.


#### Where to Go Next

**Continue to** [Control Flow - Conditionals]()

--- 

## 📚 Resources
- [The Swift Programming Language - Comments](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics#Comments)