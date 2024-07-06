# Untitled

📚Class: 

📘Subject: <a href="https://github.com/lamula21/cheat-sheets/blob/main/"></a>

✏️Section: 

🗓️Date: 2024-02-07

---

# Intro 

Create a project:

```bash
flutter create <project_name>
```

Run project:

```bash
flutter run
```

Upgrade Flutter:

```bash
flutter upgrade
flutter clean
flutter pub get
flutter pub upgrade
```

## Connect to iOS Device

Go to project folder:

```bash
open ios/Runner.xcworkspace
```

Click on the top left navbar `Runner` 
-> Signin & Capabilities 
-> Check Automatically manage signin
-> Add account to `Team`
-> Bundle identifier: create a unique id for the app
-> Click on `Run` button on the left top navbar


On the phone:
VPN -> Apple Development -> Trust
-> `Run` on the left top navbar


## Connect Wireless

Xcode -> Window (top Navbar) -> Devices and Simulators
Connect iphone and computer to same wifi
Check [x] Connect via network

Unplug iphone -> `Run` button on the left top navbar

or 

```bash
flutter run -d <device-id>
```

Device ID:

```bash
flutter devices
```


## Some knwon Errors

`iproxy` error:

dev/flutter/bin/cache/artifacts

Remove `artifacts` folder. Done
