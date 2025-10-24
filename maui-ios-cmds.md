# ios-deploy-
xcrun simctl list devices
---
dotnet clean
---
dotnet restore 
---

xcrun simctl shutdown all
---

dotnet build -t:Run -f net9.0-ios -p:_DeviceId="12AF4C35-EF32-4D98-B3D9-59A1B9444129"
---
dotnet build -t:Run -f net9.0-ios -v:diag > buildlog.txt

dotnet build -f:net6.0-ios -c Release --runtime ios-x64