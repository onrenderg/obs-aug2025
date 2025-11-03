


# For Android remote debugging
dotnet tool install -g dotnet-dsrouter
dotnet dsrouter client-server -tcps 127.0.0.1:9000 -ipcc /tmp/android-port



dotnet new maui  -f net9.0 -n TmpApp


cd C:\Program Files (x86)\Android\android-sdk\emulator

emulator -list-avds

# Start specific emulator (replace with your AVD name)
```cmd
emulator -avd pixel_7_-_api_30
dotnet build -t:Run -f net9.0-android -p:AndroidDevice="emulator-5554"
```

adb devices
scrcpy -s emulator-5554


```xml
	<!-- Android Runtime Identifiers: Include x64 for emulators and ARM for physical devices -->
		<RuntimeIdentifiers Condition="$(TargetFramework.Contains('android'))">android-x64;android-arm64</RuntimeIdentifiers>
```

## Todo 
* logcat with debug message 
* vim write all "dotnet new maui  -f net9.0 -n TmpApp" for both 
* .net ipynb polygon file update 


## local character set equivalnet logic/story same sthing 



## live pages mcp devtools 
https://github.com/ChromeDevTools/chrome-devtools-mcp/?tab=readme-ov-file#chrome-devtools-mcp

## maui navigation structer apprch
* crete chilren inheriting nav etc and then use   Children.Add(new Dashboard_Page()); this way NavigationPage.TitleView in child page redundant 
* Children.Add(new NavigationPage(new Dashboard_Page())); : NavigationPage.TitleView is an attached property that customizes the navigation bar, but it only works when a page is displayed inside a NavigationPage container.The NavigationPage.TitleView in 
xpage  is ignored because there's no NavigationPage to display it.


## Maui tags 
listview--> collectionview

frame--> border


## misc  {} incremetal docs ** 
StaticResource
AppThemeBinding Light={StaticResource Primary}, Dark={StaticResource Primary}}





## xaml elements cocnpets like grid concepts 
* HorizontalStackLayout arranges children sequentially from left to right. so need propterty                         HorizontalOptions="Start" 



## python eq : 

```mermaid
[Database Query] → Returns List<TodayVc> objects
         ↓
[Line 67-68] → Assigns to listView_ongoingvc.ItemsSource
         ↓
[XAML DataTemplate] → Each TodayVc becomes BindingContext of a Grid
         ↓                     (Shows only labelname & NoOfVc)
[User Taps Card]
         ↓
[Line 86-87] → Gets Grid.BindingContext (the full TodayVc object)
         ↓
[Line 92] → Accesses currentRecord.Startingtime
                    ↑
                    This property exists in the object
                    even though it's not shown in UI!
```


[[nicvcPy]]


##################


## maui base
* 1. MauiProgram.cs file
* 2. AppShell or App.xaml based on approched used for app nav 
* 3. using app.xaml 
    * to use use Navigation.PushAsync() put given page in NavigationPage()  so wrap MainPage in a NavigationPage: in CreateWindow method  Adds MainPage to navigation stack (as root page)
    return new Window(new NavigationPage(new MainPage()));
* navigation for default prj default page MainPage usng Wrap Page in NavigationPage







#
The user wants a complete, natural language explanation of the protected override Window CreateWindow(IActivationState? activationState) method, including all the context needed to understand it - the concepts, where it's placed, what it does, etc.

Let me break this down in a comprehensive way that explains:

The context (where it is, what class, inheritance)
Each keyword and what it means
What the method does
The parameter
The return type
Why it's needed


## moe expreince 
= 
logic part unique block be/w pages   not pattern that remain same like in  boiler app
     x:Class="TmpApp.TmpPageOne" changse 
                  Title="Tmp Page One"> chages 
                  layout is snippets so  remain same 



## Win sinstall 
winget install clink
winget install --id Microsoft.PowerToys


## Win sinstall 
## reverse history search feature

winget install clink
clink autorun install
clink autorun show
clink autorun uninstall
"C:\Program Files (x86)\clink\clink_x64.exe"
echo %PATH%
winget install --id Microsoft.PowerToys

