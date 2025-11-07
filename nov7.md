if login not prachiya 
if login 
if in prefrence  = 0 then preference 
else dashboard page 

 ./local-gitingest -exclude .log,.tmp,.bak -o my_repo.txt -size-limit -max-size 102400

# concise if else type logic docs



## nl 

```cs

 async void Btn_GenerateOTP_Clicked(System.Object sender, System.EventArgs e)
        {
            var m = App.LableValueGeneric("Mobile_ValidMobileNo");
            if (string.IsNullOrEmpty(Entry_Mobile.Text))
            {
                
                await DisplayAlert(App.AppName, m, App.Btn_OK);
                return;
            }
            try
            {
                if (Int64.Parse(Entry_Mobile.Text) < 6000000000)
                {
                    await DisplayAlert(App.AppName, m, App.Btn_OK);
                    return;
                }
            }
            catch (Exception)
            {
                await DisplayAlert(App.AppName, m, App.Btn_OK);
                return;
            }
            
            if (Btn_GenerateOTP.Text != App.LableValueGeneric("Mobile_ResendOTP"))
            {
                Loading_activity.IsVisible = true;
                var service = new Models.HitService();
                if (await service.OTP_Post(Entry_Mobile.Text) == 201)
                {
                    Entry_Mobile.IsReadOnly = true; 
                    Stack_OTP.IsVisible = true;
                    Loading_activity.IsVisible = false;
                    Lbl_EnterOTP.Text= $"{App.LableValueGeneric("EnterOTPSentonMobileNumber")} '{Entry_Mobile.Text}' {App.LableValueGeneric("withOTPID")} '{Preferences.Get("otp_id", "xxxx")}'";
                    Entry_OTP.Placeholder = $"{Preferences.Get("otp_id", "xxxx")}";
                    Device.StartTimer(new TimeSpan(0, 0, 1), () =>
                    {
                        TimeInSecond = TimeInSecond - 1;
                        if (TimeInSecond != 0)
                        {
                            Btn_GenerateOTP.Text = $"{App.LableValueGeneric("Mobile_ResendOTP")} {TimeInSecond} S";
                            return true;
                        }
                        else
                        {
                            TimeInSecond = 60;
                            Btn_GenerateOTP.Text = $"{App.LableValueGeneric("Mobile_ResendOTP")}";
                            return false;
                        }
                    });
                }
                Loading_activity.IsVisible = false;
            }
            Loading_activity.IsVisible = false;
        }


```

Here is a line-by-line explanation of the `Btn_GenerateOTP_Clicked` function from the file `MainPage.xaml.cs`.

### ➡️ Function Definition

[cite_start]`async void Btn_GenerateOTP_Clicked(System.Object sender, System.EventArgs e)` [cite: 558]

* **Natural Language:** This line defines the function.
    * `async` means this function can perform tasks in the background (like calling a server) without freezing the app's user interface.
    * `Btn_GenerateOTP_Clicked` is the function's name. [cite_start]This name is linked to the `Clicked` property of the "Generate OTP" button in the `MainPage.xaml` file[cite: 537]. This function runs every time that button is tapped.

---

### ➡️ Validation (Lines 1-13)

[cite_start]`var m = App.LableValueGeneric("Mobile_ValidMobileNo");` [cite: 558]

* **Natural Language:** This line gets an error message from the app's internal database and stores it in a variable named `m`.
    * [cite_start]It calls the `LableValueGeneric` function (defined in `App.xaml.cs`)[cite: 130].
    * [cite_start]That function looks up the ID "Mobile\_ValidMobileNo" in the `FormLabels` SQLite database [cite: 906] to get the correct text for the user's selected language (e.g., "Please provide a valid mobile number").

[cite_start]`if (string.IsNullOrEmpty(Entry_Mobile.Text))` [cite: 559]

* **Natural Language:** This checks if the user left the mobile number textbox empty.
    * [cite_start]`Entry_Mobile` is the name of the `Entry` (textbox) element defined in `MainPage.xaml`[cite: 537].
    * `.Text` gets the text the user typed into it.
    * `string.IsNullOrEmpty` is a C# command that returns `true` if the textbox is empty or just has spaces.

[cite_start]`await DisplayAlert(App.AppName, m, App.Btn_OK);` [cite: 559]

* **Natural Language:** If the textbox was empty, this line shows a pop-up alert message.
    * `await` pauses the function here until the user interacts with the pop-up.
    * [cite_start]`App.AppName` (from `App.xaml.cs`) [cite: 104] is used as the alert's title (e.g., "Grievance Appellate Committee").
    * `m` is the error message we just retrieved (e.g., "Please provide a valid mobile number").
    * [cite_start]`App.Btn_OK` (from `App.xaml.cs`) [cite: 105] provides the text for the alert's button (e.g., "OK").

[cite_start]`return;` [cite: 560]

* **Natural Language:** This immediately stops the function. Since the user didn't enter a number, there is no point in continuing.

[cite_start]`try { ... }` [cite: 560]

* **Natural Language:** This starts a "try" block. This is a safety measure. It tells the app to *try* running the code inside it, but be prepared for it to fail (or "throw an exception").

[cite_start]`if (Int64.Parse(Entry_Mobile.Text) < 6000000000)` [cite: 560]

* **Natural Language:** This checks if the mobile number is a plausible 10-digit number.
    * `Int64.Parse` tries to convert the text from the `Entry_Mobile` box into a large number. This will crash if the user typed letters (which is why it's in a `try` block).
    * It then checks if that number is less than 6,000,000,000. This is a simple check to ensure the number is a 10-digit number that doesn't start with 0-5.

[cite_start]`await DisplayAlert(App.AppName, m, App.Btn_OK);` [cite: 561]
[cite_start]`return;` [cite: 561]

* [cite_start]**Natural Language:** If the number is not valid (e.g., "12345"), it shows the same error message [cite: 561] [cite_start]and stops the function[cite: 561].

[cite_start]`catch (Exception) { ... }` [cite: 561]

* **Natural Language:** This is the "catch" block. If the code inside `try` crashed (for example, if `Int64.Parse` failed because the user entered "abc"), the app jumps directly to this block instead of crashing.

[cite_start]`await DisplayAlert(App.AppName, m, App.Btn_OK);` [cite: 562]
[cite_start]`return;` [cite: 562]

* **Natural Language:** This code runs only if the `try` block failed. [cite_start]It shows the "Please provide a valid mobile number" alert [cite: 562] [cite_start]and stops the function[cite: 562].

---

### ➡️ API Call and Timer (Lines 14-41)

[cite_start]`if (Btn_GenerateOTP.Text != App.LableValueGeneric("Mobile_ResendOTP"))` [cite: 562]

* **Natural Language:** This checks if the timer is already running.
    * [cite_start]`Btn_GenerateOTP` is the button itself[cite: 537].
    * Later in this function, the button's text is changed to "Resend OTP" while a timer counts down.
    * This `if` statement ensures that the app only tries to send a new OTP if the button's text is *not* "Resend OTP" (meaning, the timer is not active).

[cite_start]`Loading_activity.IsVisible = true;` [cite: 563]

* **Natural Language:** This displays the "Please Wait..." loading spinner.
    * [cite_start]`Loading_activity` is a `ContentView` element in `MainPage.xaml` [cite: 543] that covers the screen. Setting `IsVisible` to `true` makes it appear.

[cite_start]`var service = new Models.HitService();` [cite: 563]

* **Natural Language:** This creates a new "service" object. [cite_start]The `HitService` class (defined in another file) [cite: 31, 44, 563, 572] contains all the code for communicating with the application's backend server (the API).

[cite_start]`if (await service.OTP_Post(Entry_Mobile.Text) == 201)` [cite: 563]

* **Natural Language:** This line tells the service to request an OTP from the server.
    * It calls the `OTP_Post` function inside the `HitService` object, passing it the mobile number from the textbox.
    * `await` pauses the function here, waiting for the server to respond.
    * The server will send back a status code. A code of `201` means "Created," which indicates the server successfully generated and sent the OTP. The code inside this `if` block will only run if the call was successful.

[cite_start]`Entry_Mobile.IsReadOnly = true;` [cite: 563]

* [cite_start]**Natural Language:** This locks the mobile number textbox (`Entry_Mobile`) [cite: 537] so the user can't change the number after the OTP is sent.

[cite_start]`Stack_OTP.IsVisible = true;` [cite: 564]

* **Natural Language:** This makes the hidden OTP entry section visible.
    * [cite_start]`Stack_OTP` is a `StackLayout` container in `MainPage.xaml` [cite: 538] that holds the "Enter OTP" label and the OTP textbox.

[cite_start]`Loading_activity.IsVisible = false;` [cite: 564]

* [cite_start]**Natural Language:** The server has responded, so this line hides the "Please Wait..." loading spinner[cite: 543].

[cite_start]`Lbl_EnterOTP.Text = $"{...}";` [cite: 564]

* [cite_start]**Natural Language:** This updates the "Enter OTP" label (`Lbl_EnterOTP`) [cite: 538] with detailed instructions.
    * [cite_start]It combines text from the language database (like "Enter OTP Sent on Mobile Number") with the user's actual mobile number and an "OTP ID" that was saved to the device's `Preferences` by the `HitService`[cite: 564].

[cite_start]`Entry_OTP.Placeholder = $"{...}";` [cite: 564]

* [cite_start]**Natural Language:** This sets the gray placeholder text inside the OTP textbox (`Entry_OTP`) [cite: 538] [cite_start]to show the "OTP ID"[cite: 564], making it easier for the user to reference.

[cite_start]`Device.StartTimer(new TimeSpan(0, 0, 1), () => { ... });` [cite: 565]

* **Natural Language:** This starts a timer that will run a block of code (the part in `() => { ... }`) every **1 second**.

[cite_start]`TimeInSecond = TimeInSecond - 1;` [cite: 565]

* **Natural Language:** This is inside the timer. [cite_start]It subtracts 1 from the `TimeInSecond` variable (which was set to 60 at the top of the file)[cite: 546].

[cite_start]`if (TimeInSecond != 0)` [cite: 566]

* **Natural Language:** This checks if the countdown has reached zero.

[cite_start]`Btn_GenerateOTP.Text = $"{...}";` [cite: 566]

* [cite_start]**Natural Language:** If the timer is *not* zero, this updates the button's text to show a countdown (e.g., "Resend OTP 59 S")[cite: 566].

[cite_start]`return true;` [cite: 567]

* **Natural Language:** This tells the timer: "Keep running and come back here in another second."

[cite_start]`else { ... }` [cite: 567]

* **Natural Language:** This code runs only when `TimeInSecond` finally reaches 0.

[cite_start]`TimeInSecond = 60;` [cite: 567]

* [cite_start]**Natural Language:** This resets the countdown variable back to 60 for the next time[cite: 567].

[cite_start]`Btn_GenerateOTP.Text = $"{...}";` [cite: 568]

* [cite_start]**Natural Language:** This changes the button's text to "Resend OTP" (without the number)[cite: 568]. This also "unlocks" the button, allowing the user to press it again.

[cite_start]`return false;` [cite: 568]

* **Natural Language:** This tells the timer: "Stop running."

[cite_start]`Loading_activity.IsVisible = false;` [cite: 569, 570]

* **Natural Language:** These are final cleanup lines. [cite_start]If the API call failed (the `if` check on line 21 was false) [cite: 563][cite_start], or if the user clicked the button while the timer was active, this ensures the loading spinner is hidden[cite: 569, 570].