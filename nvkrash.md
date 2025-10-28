The issue is clear. The PersonalinforPage is being used in two different contexts:

1. As a tab in a TabbedPage (when it's part of NICVCTabbedPage)
2. As a standalone page navigated to from AboutUsPage

When it's navigated to from AboutUsPage, the Parent is a NavigationPage, not a TabbedPage. That's why the cast fails.

Looking at the code:

- Line 177: `var tabbedPage = (TabbedPage)Parent;` - This assumes Parent is always a TabbedPage
- Lines 160 and 170: The save/update buttons use `await Navigation.PopAsync();` which is the correct way to go back

The cancel button should do the same - just pop the current page from navigation stack instead of trying to switch tabs.

## Fix







**✅ Fixed! InvalidCastException Resolved**

The issue was that [PersonalinforPage](cci:2://file:///c:/Users/parth/Desktop/maui/nicvc-basetwo-git/NICVC/PersonalinforPage.xaml.cs:13:4-287:5) is used in **two different contexts**:

1. **As a tab** in `NICVCTabbedPage` (Parent is TabbedPage)
2. **As a navigated page** from [AboutUsPage](cci:2://file:///c:/Users/parth/Desktop/maui/nicvc-basetwo-git/NICVC/AboutUsPage.xaml.cs:10:4-286:5) using `Navigation.PushAsync()` (Parent is NavigationPage)

## The Problem:
The original code at line 177 always tried to cast `Parent` to `TabbedPage`, which failed when the page was navigated to from AboutUsPage.

## The Solution:
Updated [btn_cancel_Clicked](cci:1://file:///c:/Users/parth/Desktop/maui/nicvc-basetwo-git/NICVC/PersonalinforPage.xaml.cs:173:8-189:9) method (lines 174-190) to:

1. **First check** if the page is in a navigation stack (`Navigation.NavigationStack.Count > 1`)
   - If yes → Use `await Navigation.PopAsync()` to go back
   
2. **Otherwise** check if Parent is a TabbedPage using safe cast (`is TabbedPage`)
   - If yes → Switch to the dashboard tab

Now the Cancel button will work correctly in both scenarios:
- ✅ When navigated from AboutUsPage (uses PopAsync)
- ✅ When it's a tab in TabbedPage (switches tabs)

The InvalidCastException is now prevented! 🎯