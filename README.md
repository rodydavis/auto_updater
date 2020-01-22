# auto_updater

An auto updating example built for Flutter Desktop that uses Sparkle.

### MacOS

- Source: https://github.com/sparkle-project/Sparkle
- Info: https://sparkle-project.org

### Windows

- Source: https://github.com/vslavik/winsparkle
- Info: https://winsparkle.org

## Getting Started

You can easily just download the project and replace the feed url if you wish! Or fork the project template.

### MacOS Setup

More info here: https://sparkle-project.org/documentation/

Add Sparkle to your MacOS `macos/Podfile`

```ruby
target 'Runner' do
  use_frameworks!
  use_modular_headers!
  
  # Extra Pods
  pod 'Sparkle' # <-- Add This Line
```

Open `macos/Runner/info.plist` and add the following keys:

```xml
<key>SUFeedURL</key>
<string>YOUR_FEED_URL</string>
<key>SUEnableAutomaticChecks</key>
<true/>
```

Replace `YOUR_FEED_URL` with your [AppCast](https://github.com/vslavik/winsparkle/wiki/Appcast-Feeds) url. You can test by using [this demo feed](https://sparkle-project.org/files/sparkletestcast.xml).

Open `macos/Runner/MainFlutterWindow.swift` and modify it to look like this:

```swift
import Cocoa
import FlutterMacOS

import Sparkle

class MainFlutterWindow: NSWindow {

    @IBAction func checkForUpdates(_ sender: Any) {
        let updater = SUUpdater.shared()
        updater?.feedURL = URL(string: "YOUR_FEED_URL")
        updater?.checkForUpdates(self)
    }

    override func awakeFromNib() {
        let flutterViewController = FlutterViewController.init()
        let windowFrame = self.frame
        self.contentViewController = flutterViewController
        self.setFrame(windowFrame, display: true)

        RegisterGeneratedPlugins(registry: flutterViewController)

        super.awakeFromNib()
    }
}

```

Open the application worspace `macos/Runner.xcworkspace`.

Add a menu item:

![image](/doc/screenshots/1.png)
![image](/doc/screenshots/2.png)

Add a new opbject: 

![image](/doc/screenshots/4.png)

Change the class:

![image](/doc/screenshots/5.png)

Connect the action by holding shift:

![image](/doc/screenshots/6.png)
