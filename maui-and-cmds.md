# dotent-build-run
_start ms-settings:developers_
## Android

```xml
<TargetFrameworks>net8.0-android;net8.0-ios;net8.0-maccatalyst</TargetFrameworks>

<TargetFrameworks Condition="$([MSBuild]::IsOSPlatform('windows'))">$(TargetFrameworks);net8.0-windows10.0.19041.0</TargetFrameworks>

```
cmd 
dotnet clean 

dotnet build -t:Run -f net8.0-android /-c Release/Debug

||
dotnet build -t:Run -f net9.0-windows10.0.19041.0
# List all connected devices first

adb devices

# Then target specific device

dotnet build -t:Run -f net8.0-android -p:AndroidDevice=2826171100004597

dotnet build -t:Run -f net9.0-android -p:RuntimeIdentifier=android-arm64 -p:AndroidDevice=2826171100004597


# Test prj 

dotnet new maui -n MauiButtonApp


adb shell getprop ro.product.cpu.abi
armeabi-v7a


dotnet clean
dotnet build -t:Run -f net9.0-android -p:AndroidDevice=2826171100004597 -p:RuntimeIdentifier=android-arm -p:AndroidFastDeploymentType=None



#  CustomDefault 

C:\Program Files (x86)\Android\android-sdk\

dotnet build -t:InstallAndroidDependencies -f net8.0-android -p:AndroidSdkDirectory=c:\work\android-sdk -p:JavaSdkDirectory=c:\work\jdk -p:AcceptAndroidSdkLicenses=True

https://learn.microsoft.com/en-us/dotnet/android/getting-started/installation/dependencies


[[deploy-dsf]]


# Add to PATH for current session
$env:Path += ";C:\Program Files (x86)\Android\android-sdk\emulator"
$env:Path += ";C:\Program Files (x86)\Android\android-sdk\platform-tools"

# Now you can use directly
emulator -list-avds
adb devices


# Nopth
"C:\Program Files (x86)\Android\android-sdk\emulator\emulator.exe" -list-avds   
pixel_7_-_api_30

"C:\Program Files (x86)\Android\android-sdk\emulator\emulator.exe" -avd pixel_7_-_api_30   

adb devices


dotnet clean  
dotnet restore  
dotnet build -t:Run -f net9.0-android

adb logcat | Select-String "MauiApp1"


@id:ms-dotnettools.dotnet-maui