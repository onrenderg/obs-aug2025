For Android emulator and deployment from terminal on Windows, here are the commands:

## **Android Emulator & Deployment Commands**

### **1. List Available Emulators**
```powershell
# List all AVDs (Android Virtual Devices)
emulator -list-avds
```

### **2. Start Android Emulator**
```powershell
# Start specific emulator (replace with your AVD name)
emulator -avd Pixel_5_API_34

# Or start in background
Start-Process emulator -ArgumentList "-avd","Pixel_5_API_34"
```

### **3. List Connected Devices**
```powershell
# List all connected devices/emulators
adb devices
```

### **4. Build & Deploy to Android**
```powershell
# Clean
dotnet clean

# Restore
dotnet restore

# Build for Android
dotnet build -f net9.0-android

# Build and Run on emulator/device
dotnet build -t:Run -f net9.0-android

# Build with specific device (get device ID from 'adb devices') 
dotnet build -t:Run -f net9.0-android  -p:AndroidDevice="R9ZY40RDV0K"  -c Debug

# Power shell

@"
{
  "sdk": {
    "version": "6.0.428",
    "rollForward": "latestPatch"
  }
}
"@ | Out-File -FilePath "global.json" -Encoding utf8
dotnet workload install android


# Xamrain 
dotnet --list-sdks
dotnet build -t:Run -f net6.0-android -p:AndroidDevice="R9ZY40RDV0K" -c Debug
dotnet workload install android

# Build Release APK
dotnet build -f net9.0-android -c Release

# Publish APK
dotnet publish -f net9.0-android -c Release
```

### **5. Install APK Manually**
```powershell
# After building, install APK to running emulator
adb install "bin\Debug\net9.0-android\com.companyname.mauiapp1-Signed.apk"

# Or for release
adb install "bin\Release\net9.0-android\publish\com.companyname.mauiapp1-Signed.apk"
```

### **6. View Logs (like iOS console)**
```powershell
# View Android logcat
adb logcat

# Filter for your app
adb logcat | Select-String "MauiApp1"

# Clear logs first
adb logcat -c
adb logcat
```

### **7. Stop Emulator**
```powershell
# Kill all emulators
adb -s emulator-5554 emu kill

# Or close all
adb devices | Select-String "emulator" | ForEach-Object { adb -s $_.Line.Split()[0] emu kill }
```

### **Complete Workflow Example**
```powershell
# 1. List available emulators
emulator -list-avds

# 2. Start emulator (replace with your AVD name)
Start-Process emulator -ArgumentList "-avd","Pixel_5_API_34"

# 3. Wait for emulator to boot, then check
adb devices

# 4. Clean and build
dotnet clean
dotnet restore
dotnet build -t:Run -f net9.0-android

# 5. View logs
adb logcat | Select-String "MauiApp1"
```

### **If You Don't Have Emulators Set Up**
```powershell
# Open Android SDK Manager to create AVD
sdkmanager --list

# Or use Android Studio AVD Manager
# Run: studio.exe (if Android Studio is installed)
```

### **Diagnostic Build (like your iOS example)**
```powershell
dotnet build -t:Run -f net9.0-android -v:diag > buildlog.txt
```

**Note:** Make sure Android SDK tools are in your PATH. You can verify with:
```powershell
adb --version
emulator -version
```

Try starting with `emulator -list-avds` to see what emulators you have available!