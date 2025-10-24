```cmd
adb -s R9ZY40RDV0K logcat -c adb -s R9ZY40RDV0K logcat | findstr -i "AndroidRuntime.*at " adb -s R9ZY40RDV0K logcat | findstr -i "AndroidRuntime.*at "
```


vs extension : 
@id:ms-dotnettools.csdevkit
@id:ms-dotnettools.dotnet-maui


# Approahc 

sequence of method calls that led to the current breakpoint = callstack 
eg  : MauiApp1.dll!MauiApp1.MainPage.OnCounterClicked