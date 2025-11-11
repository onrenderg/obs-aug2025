# API Request Structure in MAUI C# Code

Let me break down how API requests are formatted in your MAUI app:

## 1. Basic HTTP Request Pattern

```csharp
public async Task<int> MethodName(string parameter)
{
    // Step 1: Check Internet Connection
    var current = Connectivity.NetworkAccess;
    if (current == NetworkAccess.Internet)
    {
        try
        {
            // Step 2: Create HttpClient
            var client = new HttpClient();
            
            // Step 3: Add Authentication Headers
            var byteArray = Encoding.ASCII.GetBytes("username:password");
            client.DefaultRequestHeaders.Authorization = 
                new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
            
            // Step 4: Prepare Request Body (JSON)
            string jsonData = JsonConvert.SerializeObject(new
            {
                property1 = "value1",
                property2 = parameter
            });
            
            // Step 5: Create StringContent with JSON
            StringContent content = new StringContent(
                jsonData,           // JSON string
                Encoding.UTF8,      // Encoding
                "application/json"  // Content-Type
            );
            
            // Step 6: Send Request (POST/GET/PUT)
            HttpResponseMessage response = await client.PostAsync(
                "https://api.example.com/endpoint",
                content
            );
            
            // Step 7: Read Response
            var result = await response.Content.ReadAsStringAsync();
            
            // Step 8: Parse JSON Response
            var parsed = JObject.Parse(result);
            
            // Step 9: Handle Response Based on Status Code
            if ((int)response.StatusCode == 200)
            {
                // Success logic
                return 200;
            }
            else
            {
                // Error logic
                return 500;
            }
        }
        catch (Exception ex)
        {
            // Handle exceptions
            return 500;
        }
    }
    else
    {
        // No internet
        await App.Current.MainPage.DisplayAlert("Error", "No Internet", "OK");
        return 101;
    }
}
```

## 2. Object Initialization Types

### Anonymous Objects (for JSON)
```csharp
// Inline anonymous object - commonly used for API payloads
var requestBody = new
{
    username = "john",
    password = "secret",
    age = 25
};

string json = JsonConvert.SerializeObject(requestBody);
// Result: {"username":"john","password":"secret","age":25}
```

### Named Objects (Models)
```csharp
// Define a class first
public class User
{
    public string Username { get; set; }
    public string Password { get; set; }
    public int Age { get; set; }
}

// Then create and use it
var user = new User
{
    Username = "john",
    Password = "secret",
    Age = 25
};

string json = JsonConvert.SerializeObject(user);
```

## 3. HTTP Objects Creation

### HttpClient
```csharp
// Basic creation
var client = new HttpClient();

// With timeout
var client = new HttpClient
{
    Timeout = TimeSpan.FromSeconds(30)
};

// With base address
var client = new HttpClient
{
    BaseAddress = new Uri("https://api.example.com/")
};
```

### Headers
```csharp
// Basic Auth
var authBytes = Encoding.ASCII.GetBytes("username:password");
var authHeader = Convert.ToBase64String(authBytes);
client.DefaultRequestHeaders.Authorization = 
    new AuthenticationHeaderValue("Basic", authHeader);

// Bearer Token
client.DefaultRequestHeaders.Authorization = 
    new AuthenticationHeaderValue("Bearer", "your_token_here");

// Custom Headers
client.DefaultRequestHeaders.Add("X-Custom-Header", "value");
client.DefaultRequestHeaders.Accept.Add(
    new MediaTypeWithQualityHeaderValue("application/json")
);
```

### StringContent (Request Body)
```csharp
// JSON content
StringContent content = new StringContent(
    jsonString,           // Your JSON data
    Encoding.UTF8,        // Character encoding
    "application/json"    // MIME type
);

// Form data
var formData = new FormUrlEncodedContent(new[]
{
    new KeyValuePair<string, string>("key1", "value1"),
    new KeyValuePair<string, string>("key2", "value2")
});
```

## 4. HTTP Methods

### POST Request
```csharp
HttpResponseMessage response = await client.PostAsync(
    "https://api.example.com/create",
    content  // StringContent object
);
```

### GET Request
```csharp
HttpResponseMessage response = await client.GetAsync(
    "https://api.example.com/data?id=123"
);
```

### PUT Request
```csharp
HttpResponseMessage response = await client.PutAsync(
    "https://api.example.com/update",
    content
);
```

### DELETE Request
```csharp
HttpResponseMessage response = await client.DeleteAsync(
    "https://api.example.com/delete/123"
);
```

## 5. Response Handling

### Reading Response
```csharp
// As string
var result = await response.Content.ReadAsStringAsync();

// As byte array
var bytes = await response.Content.ReadAsByteArrayAsync();

// As stream
var stream = await response.Content.ReadAsStreamAsync();
```

### Parsing JSON Response
```csharp
// Using JObject (dynamic)
var parsed = JObject.Parse(result);
var value = parsed["propertyName"].ToString();

// Using JArray (for arrays)
var array = JArray.Parse(result);
foreach (var item in array)
{
    var id = item["id"].ToString();
}

// Deserialize to object
var myObject = JsonConvert.DeserializeObject<MyClass>(result);
```

### Status Code Handling
```csharp
// Check by value
if ((int)response.StatusCode == 200)
{
    // Success
}

// Check by enum
if (response.StatusCode == System.Net.HttpStatusCode.OK)
{
    // Success
}

// Get status code as int
int statusCode = (int)response.StatusCode;
```

## 6. Complete Real Example from Your Code

```csharp
public async Task<int> AadharNameAndNumberVerification_Post(
    string _aadhaarNumber, 
    string _AadhaarName)
{
    var current = Connectivity.NetworkAccess;
    if (current == NetworkAccess.Internet)
    {
        try
        {
            // 1. Create HTTP client
            var client = new HttpClient();
            
            // 2. Add Basic Authentication
            var byteArray = Encoding.ASCII.GetBytes(
                Preferences.Get("BasicAuth", "xx:xx")
            );
            client.DefaultRequestHeaders.Authorization = 
                new AuthenticationHeaderValue(
                    "Basic", 
                    Convert.ToBase64String(byteArray)
                );

            // 3. Create request payload (anonymous object)
            string jsonData = JsonConvert.SerializeObject(new
            {
                password = "Welcome@123",
                aadhaarNumber = _aadhaarNumber,
                txnRequestID = Guid.NewGuid().ToString().Trim(),
                bioAuth = "n",
                demoAuth = "y",
                name = _AadhaarName
            });
            
            // 4. Encrypt the data
            string encryptedData = App.Encrypt(
                jsonData, 
                "df0025ae-77d8-4806-aa72-ee7610b00bf5"
            );
            
            // 5. Wrap encrypted data (nested object)
            string finalJson = JsonConvert.SerializeObject(new
            {
                serviceId = "10003",
                data = encryptedData
            });
            
            // 6. Create StringContent
            StringContent content = new StringContent(
                finalJson, 
                Encoding.UTF8, 
                "application/json"
            );

            // 7. Send POST request
            HttpResponseMessage response = await client.PostAsync(
                "https://authenticate.epramaan.gov.in/authwebservice/requestauth/v3",
                content
            );
            
            // 8. Read response
            var result = await response.Content.ReadAsStringAsync();
            
            // 9. Parse and handle response
            if ((int)response.StatusCode == 200)
            {
                try
                {
                    var parsed = JObject.Parse(result);
                    
                    if ((parsed["status"].ToString().ToLower() ?? "").Trim() == "true")
                    {
                        return 200;
                    }
                    else
                    {
                        await App.Current.MainPage.DisplayAlert(
                            App.AppName, 
                            result, 
                            App.Btn_OK
                        );
                        return 300;
                    }
                }
                catch (JsonReaderException)
                {
                    // Handle plain text error
                    return 500;
                }
            }
            
            return (int)response.StatusCode;
        }
        catch (Exception ex)
        {
            // Handle exception
            return 500;
        }
    }
    else
    {
        // No internet
        return 101;
    }
}
```

## 7. Common Patterns

### Query Parameters in GET
```csharp
// Method 1: String interpolation
var url = $"https://api.example.com/users?id={userId}&name={userName}";
var response = await client.GetAsync(url);

// Method 2: UriBuilder
var builder = new UriBuilder("https://api.example.com/users");
builder.Query = $"id={userId}&name={userName}";
var response = await client.GetAsync(builder.Uri);
```

### Error Handling
```csharp
try
{
    var response = await client.PostAsync(url, content);
    
    if (response.IsSuccessStatusCode)
    {
        // 2xx status codes
        var result = await response.Content.ReadAsStringAsync();
    }
    else
    {
        // 4xx or 5xx status codes
        var error = await response.Content.ReadAsStringAsync();
    }
}
catch (HttpRequestException ex)
{
    // Network error
}
catch (TaskCanceledException ex)
{
    // Timeout
}
catch (Exception ex)
{
    // Other errors
}
```

## Summary

**Key Components:**
1. **HttpClient** - makes HTTP requests
2. **AuthenticationHeaderValue** - adds auth headers
3. **Anonymous objects** - create JSON payloads
4. **JsonConvert.SerializeObject()** - convert objects to JSON
5. **StringContent** - wrap JSON for HTTP body
6. **await client.PostAsync()** - send request
7. **response.Content.ReadAsStringAsync()** - get response
8. **JObject.Parse()** - parse JSON response

This is the standard pattern for REST API calls in MAUI/Xamarin!