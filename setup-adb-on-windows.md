[🏠 Home](https://kevin109.github.io/)

# Set up ADB on Windows by following the tutorial

Setting up ADB (Android Debug Bridge) on a Windows system is essential for developers working with embedded Android platforms such as Rockchip-based SBCs. This tutorial walks you through the step-by-step process of downloading, installing, and configuring ADB to enable USB debugging, firmware flashing, and log access. Whether you’re integrating a TFT LCD module, testing Android firmware, or customizing BSP layers, a reliable ADB setup is the foundation for smooth development and debugging.

---
## Install ADB on Windows

### 1. Download the ADB Installation Package
Different Windows environments may behave differently with each version of ADB. If one version does not work on your machine, try the other.

[adb-v1.0.39.zip](/download/adb-v1.0.39.zip) version 1.0.39 - Alternative version in case of compatibility issues

[adb-v1.0.41.zip](/download/adb-v1.0.41.zip) version 1.0.41 - Tested and works in most cases

⚠️ Note: The most suitable version depends on your system environment. We suggest starting with v1.0.41.

### 2. Extract the ZIP File
Unzip the downloaded package to a simple and accessible location — we recommend `C:\adb` for convenience.
Your folder structure should look like this:

```text
C:\adb
 |adb.exe
 |AdbWinApi.dll
 |AdbWinUsbApi.dll
```

📁 Tip: Avoid placing ADB in deeply nested folders to prevent path or permission issues later.
### 3. Add ADB to the System PATH Variable

To use ADB from any command prompt, you need to add its folder (e.g., D:\adb) to your system’s PATH environment variable:
1.	Open the Start Menu, search for Environment Variables, and click “Edit the system environment variables”.
2.	In the System Properties window, click the “Environment Variables…” button.
3.	Under System variables, find and select Path, then click Edit….
4.	Click New and enter the full path to your ADB folder, such as:

```text
D:\adb
```

5.	Click OK to save and close all windows.

<img src="/images/2023-08-30_151940_3214020.44115000558404527.png" alt="Environment setup" style="max-width: 100%; height: auto;" />
<img src="/images/2023-08-30_151815_0390640.02988313158176603.png" alt="Environment setup" style="max-width: 100%; height: auto;" />

### 4. Verify ADB Installation
To confirm ADB is installed correctly:
1.	Press Win + R, type cmd, and press Enter to open the Command Prompt.
2.	In the terminal, run the following command:

```bash
adb devices
```

3.	If ADB is set up properly, you’ll see a list of connected devices (or an empty list if no device is connected yet), like below:

Open Command Prompt（cmd） and run command `adb devices`

<img src="/images/2023-08-30_152802_9306390.23540734979466404.png" alt="Environment setup" style="max-width: 100%; height: auto;" />

✅ Tip: If you see a message like adb is not recognized as an internal or external command, double-check your system PATH setting from Step 3.

## Use ADB on Rocktech Smart Devices or Embedded SBCs
To connect Rocktech devices via ADB, you’ll need to install the appropriate USB driver based on the SoC (System on Chip) used in your device.
### 1. Install the driver
#### ✅For Rockchip-based Devices
If your Rocktech product is based on one of the following SoCs:
- PX30, RK3308, RK3288, RK3566, RK3568, RK3399

Or if you’re using a Rocktech Smart Control Panel, such as:
- RK-A4E, RK-A4ES, RK-A4EPL, RK-A6E, RK-A10E,RK-T10E

Download and install the official Rockchip USB driver:

[Rockchip USB Driver.zip](/download/Rockchip_USB_Driver.zip)

#### ✅ For Allwinner-based Devices
If your device uses the following SoCs:
- A23, A33, A64, A83T, H8, R16, R528

Download and install the official Allwinner USB driver:

[Allwinner USB Driver.zip](/download/Allwinner_USB_Driver.zip)

### 2. Connect to the Smart Device 
There are two methods to establish an ADB connection with your Rocktech Smart Device. Choose the one that best fits your environment.
##### 2.1 Connect via USB Data Cable
Ensure the device is powered on and connected to your PC using a USB data cable.
<img src="/images/2023-08-30_155209_3850890.2329156398027219.png" alt="Environment setup" style="max-width: 100%; height: auto;" />

##### 2.2 Connect via Wi-Fi
Make sure both your Smart Device and PC are connected to the same local Wi-Fi network (same router or subnet).

<img src="/images/2023-08-30_163139_9836050.45092418198247275.png" alt="Environment setup" style="max-width: 100%; height: auto;" />
<img src="/images/2023-08-30_163309_5508940.6642492226795811.png" alt="Environment setup" style="max-width: 100%; height: auto;" />

Use the following command to connect ADB over Wi-Fi (replace the IP address with your device’s actual IP):
```bash
adb connect 10.0.0.89
```

<img src="/images/2023-08-30_164736_0200210.2697552630903599.png" alt="Environment setup" style="max-width: 100%; height: auto;" />

### ⚙️ 3. File Transfer Between PC and Smart Device

#### 3.1 Push a file to the Smart Device  
Sends a file from your PC to the device's internal storage (e.g. `/sdcard/`):

```bash
adb push filename /sdcard/
```

#### 3.2 Pull a file from the Smart Device
Downloads a file from the device to your current PC directory:

```bash
adb pull /sdcard/filename
```

### 4. Install APK on the Android Device
Installs an Android application (.apk file) onto the connected Smart Device:

```bash
adb install your_app.apk
```
 Tip: Use -r to reinstall without removing user data:
```bash
adb install -r your_app.apk
```

### 5. Other Common ADB Commands
Here are a few more useful operations during development and testing:

List connected devices
```bash
adb devices
```

Reboot the device
```bash
adb reboot
```

Start a shell on the device
```bash
adb shell
```

View device logs (for debugging)
```bash
adb logcat
```

Uninstall an app (replace package.name with actual package)
```bash
adb uninstall com.example.app
```


---

[🏠 Back to Home](https://kevin109.github.io/)