# dotent-build-run

## Android

cmd dotnet clean 

dotnet build -t:Run -f net8.0-android /-c Release/Debug

||

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



