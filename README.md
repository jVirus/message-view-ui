# message-view-ui [![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)

[![Build](https://github.com/jvirus/message-view-ui/workflows/Build/badge.svg)]()
[![Platforms](https://img.shields.io/badge/Platform-iOS-yellow.svg)]()
[![Language](https://img.shields.io/badge/Language-Swift_5.1-orange.svg)]()
[![Autolayout](https://img.shields.io/badge/Autolayout-Supported-blue.svg)]()
[![SPM](https://img.shields.io/badge/SPM-Supported-lightblue.svg)]()
[![License](https://img.shields.io/badge/License-MIT-blue.svg)]()

**Last Update: 03/January/2020.**

![](logo-message_view.jpg)

### If you like the project, please give it a star ⭐ It will show the creator your appreciation and help others to discover the repo.

# ✍️ About
✉️ Easy to use HUD component for iOS [activity report, success or warning messages, etc.]

# 📺 Demo
Please wait while the `.gif` files are loading... (they are about `25Mb`)

<img src="Assets/activity_demo.gif" width="24.5%"> <img src="Assets/success_demo.gif" width="24.5%"> <img src="Assets/warning_demo.gif" width="24.5%"> <img src="Assets/custom_demo.gif" width="24.5%">

# 🍱 Features

- **Easy to use** 
  - You only need to make a call to a function though `MessageView` class.
- **Flexible `API`**
  - Includes a number of customization points that allows to decorate the `MessageView` as you'd like. 
- **Styling**
  - You may implement various visual styles by conforming to `MessageViewBuilder` protocol and supplying an instance of your style to `configure` method of `MessageView` class.
- **Behavior** 
  - You may tell the component to dismiss itself after a number of seconds or do it manually.
- **Autolayout**
  - You don't need to do anything related to autolayout - the component properly handles everything.
- **customize icons**  
  - You can supply your own icon and programmatically set its color.
  
# 📚 Code Samples

### Activity 
Presents message with an activity indicator view. The intention behind this presentation is to report some long running task:

```swift
MessageView.showActivity(withMessage: "Please wait...", dismissAfter: 3.0)
```

Or you can omit the `dismissAfter` parameter and hide the `MessageView` manually by calling `hide` method:

```swift
MessageView.hide()
```

### Success
Presents a success message. The intention behind this presentation is to report that something was successful or completed:

```swift
MessageView.showSuccess(withMessage: "Success!", dismissAfter: 2.25)
```

### Warning
Presents a warning message. The intention behind this presentation is to report that something wasn't successful or failed:

```swift
MessageView.showWarning(withMessage: "Warning!", dismissAfter: 2.5)
```

### Custom
Presents a custom image above the message. The intention behind this presentation style is defined by you, the developer. For instance we can present a failure `MessageView` by providing `failureImage` and the corresponding `tintColor`:

```swift
MessageView.showCustom(image: failureImage,
                              tintColor: .red,
                              withMessage: "Something went wrong",
                              dismissAfter: 2.8)
```

### Message update
Message updates are used in order to refresh the text message inside a `MessageView` while it's presented on screen. It's useful is situations when a long running task is in progress and we need to report various stages of the progress:

```swift
MessageView.showActivity(withMessage: “Initializing the task...")

fetcher.fetch(data) { result in 
  MessageView.update(message: "Completed! Result is \(result)", dismissAfter: 3.0)
  handle(result)
}.progress { value in 
  MessageView.update(message: "Fetching: \(value)%")
}
```

### Styles
There is a protocol called `MessageViewBuilder` that defines a number of properties. By creating your own version of style or by using one of the existing styles, you can customize the visuals of the component:

```swift
MessageView.configure(with: .dark)
MessageView.configure(with: .extraLight)
MessageView.configure(with: .default)
```

Or you can use an alternative `configure` method with your own version of style type:

```swift
public struct MessageViewNightStyleBuilder: MessageViewBuilder {
    public var activityIndicatorColor: UIColor                          = .init(red: 252 / 256, green: 0.0, blue: 0.0, alpha: 1.0)
    public var messageColor: UIColor                                    = .init(red: 71 / 256, green: 68 / 256, blue: 69 / 256, alpha: 1.0)
    public var messageFont: UIFont                                      = UIFont.systemFont(ofSize: 20)
    public var animationDuration: TimeInterval                          = 0.475
    public var loadingIndicatorSize: CGFloat                            = 55
    public var loadingIndicatorInitialTransform: CGAffineTransform      = CGAffineTransform(scaleX: 0.12, y: 0.12)
    public var successColor: UIColor                                    = .init(red: 0.0, green: 134 / 256, blue: 245 / 256, alpha: 1.0)
    public var warningColor: UIColor                                    = .init(red: 245 / 256, green: 0.0, blue: 0.0, alpha: 1.0)
    public var backgroundStyle: MessageView.BackgroundStyle             = .dark
}

MessageView.configure(with: MessageViewNightStyleBuilder())
```

## Swift Package Manager

### Xcode 11+

1. Open `MenuBar` → `File` → `Swift Packages` → `Add Package Dependency...`
2. Paste the package repository url `https://github.com/jVirus/message-view-ui` and hit `Next`.
3. Select the installment rules.

After specifying which version do you want to install, the package will be downloaded and attached to your project. 

### Package.swift
If you already have a `Package.swift` or you are building your own package simply add a new dependency:

```swift
dependencies: [
    .package(url: "`https://github.com/jVirus/message-view-ui", from: "1.0.0")
]
```

## Manual 
You can always use copy-paste the sources method 😄. Or you can compile the framework and include it with your project.


# 👨‍💻 Author 
[Astemir Eleev](https://github.com/jVirus)

# 🔖 Licence
The project is available under [MIT licence](https://github.com/jVirus/message-view/blob/master/LICENSE).  
