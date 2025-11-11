



# Select and fill 


## Maui port 
* Lifecyle port 

```cs
// App.xaml.cs
protected override Window CreateWindow(IActivationState? activationState)
{
    return new Window(new AppShell());
}
```

     string AadhaarAuthentication = "https://authenticate.epramaan.gov.in/authwebservice/requestauth/v3";
            string AadhaarOTPSend = "https://authenticate.epramaan.gov.in/authwebservice/requestaadhaarotpauth/v3";
            string AadhaarOTPVerify = "https://authenticate.epramaan.gov.in/authwebservice/verifyaadhaarotpauth/v2";





if ((int)response.StatusCode == 200)
{	
	System.Diagnostics.Debug.WriteLine($"mgogo: {response}");
    await App.Current.MainPage.DisplayAlert("Title", $"{response}", "OK");




}


[[maui-api-pro]]
## Summary of the Issue

### The Problem: **Double-Encoding BasicAuth Credentials**

Your ePramaan BasicAuth credentials were stored in a special format:
```
3O+MVC0RSgx0klSvZ4/pcw==:2uS7yDJy02QGCywWXsEx7aVd+jrDBhbERipESVk+RcU=
```

This is: **`Base64(username):Base64(password)`**

### What Your Old Code Was Doing (WRONG):

```csharp
var byteArray = Encoding.ASCII.GetBytes("3O+MVC0RSgx0klSvZ4/pcw==:2uS7yDJy02QGCywWXsEx7aVd+...");
client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
```

**This caused DOUBLE ENCODING:**
1. Took Base64-encoded strings
2. Converted them to bytes
3. Encoded to Base64 AGAIN

So the server received: `Base64(Base64(username):Base64(password))` ❌

### What the New Code Does (CORRECT):

```csharp
// 1. Split by colon
var parts = basicAuthEncoded.Split(':');

// 2. Decode each Base64 part to get actual username and password
var username = Encoding.UTF8.GetString(Convert.FromBase64String(parts[0]));
var password = Encoding.UTF8.GetString(Convert.FromBase64String(parts[1]));

// 3. Combine them properly
var credentials = $"{username}:{password}";

// 4. Encode ONCE for BasicAuth header
var byteArray = Encoding.ASCII.GetBytes(credentials);
client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
```

So the server receives: `Base64(username:password)` ✅

---

## Complete Timeline of Issues:

1. **First Issue**: BasicAuth was never set → Fixed by setting it in MainActivity.cs
2. **Second Issue**: Credentials were URL-encoded (`%2B`, `%2F`, `%3D`) → Fixed by decoding them
3. **Third Issue**: Credentials were Base64-encoded username and password being double-encoded → Fixed by decoding first, then encoding properly

**Result**: ePramaan API was rejecting authentication and returning "serverError" plain text instead of JSON response.

Now it should work! 🎯
# DigitalNagrikv2 

```cs
Preferences.Set("BasicAuth", "your_epramaan_username:your_epramaan_password");

```

