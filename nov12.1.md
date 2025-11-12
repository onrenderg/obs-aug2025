






# gen signed apk 
"C:\Program Files\Microsoft Visual Studio\2022\Community\MSBuild\Current\Bin\MSBuild.exe" GACAppeal.Android\GACAppeal.Android.csproj -p:Configuration=Debug -p:AndroidUseSharedRuntime=false -p:EmbedAssembliesIntoApk=true -t:SignAndroidPackage
# install  based on app id 
adb uninstall in.nic.gacappeal
adb install "GACAppeal.Android\bin\Debug\in.nic.gacappeal.apk"      

# Debug Exception / Crashes and ? other stuff identifible ni logcat 
logcat -c 
logcat
ctr after app lauch 
adb shell monkey -p in.nic.gacappeal -c android.intent.category.LAUNCHER 1


web app uses BouncyCastle's ChaCha7539Engine


## Debug in code 

if ((int)response.StatusCode == 404)
{
    System.Diagnostics.Debug.WriteLine($"mgogo: {response}");
    await App.Current.MainPage.DisplayAlert("HttpPost", $"{response}", "OK");


}







869296604548
parth royal 



# Skey
f10 
f11


