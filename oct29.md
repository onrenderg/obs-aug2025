```cs

 async Task GetState()
 {
     var current = Connectivity.NetworkAccess;
     if (current == NetworkAccess.Internet)
     {
         Loading_activity.IsVisible = true;
         Lbl_PleaseWait.Text = App.GetLabelByKey("pleasewait");
         try
         {

             var client = new HttpClient();
             var responce = await client.GetAsync($"{App.StateUrl}");
        
             string itemJson = await responce.Content.ReadAsStringAsync();

             if (responce.IsSuccessStatusCode)
             {
                 var result = await responce.Content.ReadAsStringAsync();
                 JObject parsed = JObject.Parse(result);
                 stateMasterDatabase = new StateMasterDatabase();
                 stateMasterDatabase.DeleteStateMaster();

                 foreach (var pair in parsed)
                 {

                     if (pair.Key == "StatesList")
                     {
                         var nodes = pair.Value;
                         var item = new StateMaster();
                         item.StateID = "0";
                         item.StateName = "All States";
                         stateMasterDatabase.AddStateMaster(item);
                         foreach (var node in nodes)
                         {

                             item.StateID = AESCryptography.DecryptAES(node["StateID"].ToString());
                             item.StateName = AESCryptography.DecryptAES(node["StateName"].ToString());
                             stateMasterDatabase.AddStateMaster(item);
                         }
                     }
                 }

             }
             App.StateMasterList = stateMasterDatabase.GetStateMaster("select * from StateMaster order by StateName").ToList();
             Loading_activity.IsVisible = false;
             if (DeviceInfo.Platform == DevicePlatform.iOS)
             {
                 Application.Current.MainPage = new NavigationPage(new PreferencePage());
             }
             else
             {
                 Application.Current.MainPage = new NavigationPage(new PreferencePage())
                 {
                     BarBackgroundColor = Color.FromArgb("#2196f3"),
                     BarTextColor = Colors.WhiteSmoke
                 };
             }
             
         }
         catch (Exception ex)
         {
             Console.WriteLine($"Error: {ex.Message}");
             if (ex.InnerException != null)
                 Console.WriteLine($"Inner: {ex.InnerException.Message}");
             Loading_activity.IsVisible = false;
             await DisplayAlert(App.GetLabelByKey("Exception"), ex.Message, App.GetLabelByKey("close"));
             return;
         }
     }
     else
     {

         Loading_activity.IsVisible = false;
         await DisplayAlert(App.GetLabelByKey("NICVC"), App.GetLabelByKey("nointernet"), App.GetLabelByKey("close"));
         return;

     }

 }
 ```

# docs : 
# use only syntax non nl for known concetps charactrs to short docs : 
 * a promise like funciont using known sytax concepts packet words having story of their own with chaacter and  relationship flow  = GetState
 * using var in conditon after declration and inlization to value retuened by method for checking netowrk contivity  to be used in if else statment  starting () to check if var = access obj ? 
 * if block = if internet access then in try catch http client with certion url  from language json txt retuned value by fn   if no ssl prombles res will be ? itemJson like respiose 
 * if in if conditon if 200 parse json new instalnce of a db 

In context to code ? 

* bind Lbl_PleaseWait x:Name for label in hstack with activityindicator  = pleasewait
* try: new http client obj 's method to get res from url returned json is retuend no ssl is parsed in if block and local mvc model class is updated with data 
```json
{"StatesList":[{"StateID":"6m4zscD4JgxLTBswwUqSig==","StateName":"N4LmgReX5rSDN2bO7nVTDMzx+xvW\/UyvtGBSIt3Cf9c="},{"StateID":"qFBZDnkI4pz8P\/foNe2nhg==","StateName":"MeL+UydDfIgqhj01ViGWcQ=="},{"StateID":"HSO7GdqoOqqoPIjb0nIodQ==","StateName":"wItmKlLq2DR83Pg8NzmWveV3YF198yruxCJkuySfIx0="},{"StateID":"nq7nivRHXXp2PM9hcgkJRQ==","StateName":"JYup3I+SCGPsszcWc2f9yQ=="},{"StateID":"jExS89nlcFwZJTryqHlZQQ==","StateName":"j2+2W8STXG0ys7tZPIGRSQ=="},{"StateID":"8Ktm8soIr4HTWt3YRBIhRQ==","StateName":"Ls7BN80e5vsmnaunuesGpg=="},{"StateID":"DJZ4ETwbsOcshM4LGSPciw==","StateName":"C0K50yixco\/xUEn0KgbS+lOHFoEHJ4XhQ7q+1F6Whtk="},{"StateID":"5PvhkvyQBKAKeQZVrf5XHQ==","StateName":"Z5mh4Mj\/7Vh+WEXS\/eg+DcnFcJzevvkUQWC+UAAPzm8="},{"StateID":"wuJdloPJHNUaIMoGO6vsAw==","StateName":"wmqo+pHl0K03hEDNokY0MA=="},{"StateID":"btP0IDrd9vyuY+cE2dknaw==","StateName":"wHTK+Feh3nt4ttQKr9SxDg=="},{"StateID":"\/Zzo5gGei04qA2+7S1GVFQ==","StateName":"FbWRJ5R2yQTge0bCUZbk2w=="},{"StateID":"8CQL5irRoPM5t8rTaGoH1g==","StateName":"VoVFyfvhcL4uU4TLCfcOuQ=="},{"StateID":"ilgad35VDTQNcdeStEyjeg==","StateName":"h4VALAjL9GppUYsSCWJksmTSbMDwJkG6ysGtu+oxr\/k="},{"StateID":"BbJoJkQNmjg5sGDwQNW0Wg==","StateName":"i26Ls6Q+kDWYIXJX5JQPPiJqLC3+3JTPzc4NbwFszIU="},{"StateID":"jaeqgw3gnMvvlrCnTsx7mQ==","StateName":"AXP6spy98bLeKo0yPElorg=="},{"StateID":"Kw+RJS74Sld4hzdg\/ZzbWw==","StateName":"HPijERGn6HjEloJ0tk+tew=="},{"StateID":"h6vk+rBKfO9F3cD0h06TDg==","StateName":"WVKs0+i1ZehbaZpMueTISg=="},{"StateID":"c\/h42NG\/QlMyBpzyFUiEmQ==","StateName":"AB5rA\/njQVOo5rsE\/+C5Mg=="},{"StateID":"EU0IzcULvMnigkxyRPTT9A==","StateName":"quOnNm1P8rPe4xOrqfSACQ=="},{"StateID":"a95Th\/W19wT04Tbqy+RVNw==","StateName":"N6\/P5cHWPm5LFkVawoYnIw=="},{"StateID":"y\/Cu9cGP524K3Q\/j1eVbig==","StateName":"h7P3EHSMMs1RoqbzcLiotg=="},{"StateID":"1wJzoOX4HAnRsiZbSVljpA==","StateName":"T2+apNEORY4amhCGr932Jg=="},{"StateID":"sTKP7tPwJrRyixmsCL36Qw==","StateName":"aOfORfaku8jAURAXk4dqEA=="},{"StateID":"bteVb2wY\/Y6fJvPwnp8Yjg==","StateName":"cTL2ckBA\/qqVmqG5spZHdA=="},{"StateID":"ZtT6V4YzZYmak8XJy0+V8g==","StateName":"vbuGWSI1bl3gGHJp2uxcwg=="},{"StateID":"HsZpw+EAXyRiUT9ry657Sg==","StateName":"H9rFkeY0BO96K9VQFzRT5A=="},{"StateID":"kP+Ahzxc6xI0g7dR0JsVpg==","StateName":"0Bsf8pSKgaz9luRS0b28HQ=="},{"StateID":"uNYUAhDvSFi3zfIvH4P2Xg==","StateName":"yzwov+fbnAmAmKp1OJxeHg=="},{"StateID":"TJGgkVHa84T6jOH+h98i4A==","StateName":"faExY8iMz1Bsee\/TN+NRDQ=="},{"StateID":"cbX4Pb+FnDvxVCJDSU79OQ==","StateName":"IGlK6Ukt2soIBOrrsZampQ=="},{"StateID":"BMfnYF3atTTiCjBjBBXj5w==","StateName":"eQTs3+nP1F8IxlGa1HeNTQ=="},{"StateID":"U937Vb3SvxHsmdYrxXN9LA==","StateName":"mH8YnjlyD43nb9sL+QG7HA=="},{"StateID":"4Mjl6RIzJCrF1hbGAHoY8Q==","StateName":"pDe9K6TKsTr8GSoEEpyThw=="},{"StateID":"7BFr9MeqKi6ZAZLyGkIbTA==","StateName":"YB9JhuyTrVm3RFc4+JL04A=="},{"StateID":"L1Q+nm0iKZwMvw6QCkKcJQ==","StateName":"aGkFL2K0xDhRMGAQ5BaWWw=="},{"StateID":"3\/NjYvJoJjmHNLiVy03vcg==","StateName":"cyUDidkVuxUKPYS2pKXT+g=="},{"StateID":"2qJCkyTJsna51sdKeQfamg==","StateName":"9oWwDPa9EFxNJkRGE0UTkw=="},{"StateID":"DA79WODKetEgfZYgDhHnUA==","StateName":"09\/sNwlGR5JlWcslV1c+jQ=="},{"StateID":"sec48Gf1mrxo55NxUdGwpQ==","StateName":"9VYDOtKDpsRU8n4e\/UUjXg=="},{"StateID":"A9qO9yeir5ZqfZM\/pylcFA==","StateName":"U+3pI3CGPGWF6\/Q531US8w=="},{"StateID":"8F1mL11INDtIvf2XZ5dqCg==","StateName":"\/H5wX4CBhwukHpCPIzCV9w=="},{"StateID":"Gl2\/xwd2xLKktEcTDfVP4Q==","StateName":"KmkXob0l8D5KJRfU9eHFWQ=="}]}
```

PreferencePage