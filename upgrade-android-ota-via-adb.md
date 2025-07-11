# Upgrade Android OTA File via ADB

This guide explains how to upgrade an Android-based SBC (Smart Control Panel) using an OTA (update.zip) file via ADB.

---

## 1. Connect the Android Device
You can choose one of the following methods to connect the device to your PC:

### Option 1: Connect via USB
Connect your Android smart control panel or SBC to the PC using a USB data cable.
Run the following command to confirm the connection:
```bash
adb devices
```

### Option 2: Connect via WiFi

Ensure both the Android device and the PC are on the same network.
Connect using:
```bash
adb connect <device-ip-address>
adb devices
```
Replace <device-ip-address> with the IP of the Android device.

---

## 2. Push OTA File to Device
After connection is successful, push the OTA update file (xxx_ota.zip) to the device:
```bash
adb push xxx_ota.zip /sdcard/update.zip
```

---

## 3. Start OTA Upgrade

Open an ADB shell:
```bash
adb shell
```

Then trigger the OTA upgrade via broadcast command:
```bash
am broadcast -a com.smatek.ota.download.complete --es com.smatek.ota.download.path /storage/emulated/0/update.zip
```
✅ Note: Replace the OTA path if you used a different location or filename.

<img src="/images/OTA-upgrade-command.png" alt="OTA-upgrade-command" style="max-width: 100%; height: auto;" />
<img src="/images/OTA-upgrade.png" alt="A4ES-WIFI-IP-Address" style="max-width: 100%; height: auto;" />

## Result

After the broadcast, the device should begin processing the update. You may observe a reboot or system update UI depending on your firmware integration.


---

[🏠 Back to Home](https://kevin109.github.io/)