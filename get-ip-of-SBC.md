# How to Get the IP Address of Your SBC or Smart Device

Knowing the IP address of your device is essential for wireless ADB debugging, SSH access, or connecting to local services. This guide provides two common methods to find the IP address of your Android-based device.
---

## Method 1: Use ADB Shell + ip addr Command
If your device is connected to your computer via USB and ADB is set up correctly, follow these steps:

✅ Step 1: Connect via USB
```bash
adb devices
```
Ensure your device is listed.

✅ Step 2: Enter ADB Shell
```bash
adb shell
```
✅ Step 3: Check IP Address
Run the following command to view the IP address:
```bash
ifconfig
```

## Method 2: Find IP via Android Settings App

## Start up Android Settings App
If ADB is not available, or if you prefer a visual method, you can check the IP address directly on the device:

#### Option 1: Launch Settings via ADB
```bash
adb shell am start -a android.settings.WIFI_IP_SETTINGS
```
This command opens the network settings page directly.

#### Option 2: Tap the App Icon
	1.	Swipe up or press the Home button to open the App Drawer.
	2.	Tap the Settings icon.
	3.	Navigate to Wi-Fi / Network Settings.
	4.	Tap the connected Wi-Fi network to view the IP address.

#### Option 3: Tap the Corner 5 Times
If the Settings app icon is not available or hidden:

📌 Tip: On Rocktech control panels, you can tap the top-right corner of the screen 5 times within 5 seconds to launch the Settings app.

## Find the IP Address of Your SBC or Smart Device
Once you’ve opened the Settings app, there are two paths depending on your network connection type:
✅ Wi-Fi Connection
	1.	Go to Network & Internet → Wi-Fi.
	2.	Make sure the device is connected to a Wi-Fi network.
	3.	Tap on the connected Wi-Fi network.
	4.	The IP address will be displayed in the detailed network info section.

<img src="/images/A4ES-WIFI-IP-Address.png" alt="A4ES-WIFI-IP-Address" style="max-width: 100%; height: auto;" />

✅ Ethernet Connection
	1.	Go to Network & Internet → Ethernet.
	2.	The IP address will be shown directly under the Ethernet configuration screen.

---

[🏠 Back to Home](https://kevin109.github.io/)