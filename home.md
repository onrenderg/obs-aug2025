[[bk]]
[[todooct24+]]
[[maui-and-debug]]
[[maui-ios-cmds]]
[[maui-and-cmds]]
[[git-base]]
[[tsql-nbk]]
[[nicvctodo_karacters]]
[[nicvcPy]]
https://obsidian-base-deploy.vercel.app/cers-finflow
[[nv]]
[[oct]]
[[nvkrash]]
---

# Setup 


## SSMS 
https://sqlserverbuilds.blogspot.com/2018/01/sql-server-management-studio-ssms.html

## MSSQL 

https://sqlserverbuilds.blogspot.com/2019/01/sql-server-2019-versions.html
https://www.microsoft.com/en-us/download/details.aspx?id=108372



# maui build 
https://dotnet.microsoft.com/download/dotnet/8.0
dotnet --list-sdks

## vs-list
* @id:ms-dotnettools.csdevkit
* .net extension pack
*  sql notebook
* *sql tools
* sql tools postgresSql
* sql tools sql server 
* xaml completions 
* xaml styler 
* .net install tool

* git graph
* git history
* git history diff
* github copilot 
* github copilot chat 
* jupyter 
* jupyter cell tags 
* jupyter keymap
* jupyter notebook renderers
* juptyter slide show 
* polyglot notebooks
* pylance
* python
* python debugger
* python environments


## dotnet sdk https://dotnet.microsoft.com/en-us/download




# sql server
https://hasura.io/learn/database/microsoft-sql-server/core-concepts/2-sql-types/

## sql server auth and ip setting  **`.\SQLEXPRESS`**

## enable TCP/IP and

win+R
sqlservermanager16.msc

enable mixed mode :
ui 

Enable the `sa` Login :
ALTER LOGIN sa ENABLE;

Set or Reset the `sa` Password
ALTER LOGIN sa WITH PASSWORD = 'sec12345';
https://www.youtube.com/watch?v=p9mv2RP6Tck&t=32s

            // await Navigation.PopAsync();  // Go back

            // await Navigation.PushAsync(new MainPage());  // Push new page
             MainPage = new NavigationPage(new ParichayPage());
              MainPage = new ParichayPage();