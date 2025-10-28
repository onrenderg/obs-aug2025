**The blank page was ON CurrentMonthVcPage, not Dashboard!** Let me clarify:

## What Happened:

1. **Dashboard_Page was fine** ✅
2. User clicked "VC In Month" label on Dashboard
3. App navigated to **CurrentMonthVcPage** 
4. **CurrentMonthVcPage showed blank** ❌ (as in your screenshot)

## Why CurrentMonthVcPage Was Blank:

### **The Bug:**
```xml
<Border>
    <CollectionView x:Name="listView_schedulevc" />      ← Created in visual tree
    <CollectionView x:Name="listView_schedulevclocal" /> ← IGNORED! Not created!
</Border>
```

### **What the Code Was Doing:**
```csharp
if (App.Language == 0)
{
    listView_schedulevc.IsVisible = true;        // English - works
    listView_schedulevclocal.IsVisible = false;
}
else
{
    listView_schedulevc.IsVisible = false;
    listView_schedulevclocal.IsVisible = true;   // ❌ Trying to show element that doesn't exist!
}
```

**In your case:** You're probably using **Hindi/Local language** (App.Language != 0), so the code tried to show `listView_schedulevclocal`, but that CollectionView **never got created** because Border ignored it → **Blank page!**

### **The Fix:**
```xml
<Border>
    <Grid>  ← Grid allows multiple children
        <CollectionView x:Name="listView_schedulevc" />      ← Both exist now!
        <CollectionView x:Name="listView_schedulevclocal" /> ← Both exist now!
    </Grid>
</Border>
```

Now both CollectionViews exist, and toggling `IsVisible` works correctly! 🎯






The issue is clear. The PersonalinforPage is being used in two different contexts:

As a tab in a TabbedPage (when it's part of NICVCTabbedPage)
As a standalone page navigated to from AboutUsPage
When it's navigated to from AboutUsPage, the Parent is a NavigationPage, not a TabbedPage. That's why the cast fails.

Looking at the code:

Line 177: var tabbedPage = (TabbedPage)Parent; - This assumes Parent is always a TabbedPage
Lines 160 and 170: The save/update buttons use await Navigation.PopAsync(); which is the correct way to go back
The cancel button should do the same - just pop the current page from navigation stack instead of trying to switch tabs.
















                    <!--<Grid.ColumnDefinitions>
                        <ColumnDefinition Width="3*"/>
                        <ColumnDefinition Width="7*"/>
                    </Grid.ColumnDefinitions>-->


                    The issue is clear. The PersonalinforPage is being used in two different contexts:

As a tab in a TabbedPage (when it's part of NICVCTabbedPage)
As a standalone page navigated to from AboutUsPage
When it's navigated to from AboutUsPage, the Parent is a NavigationPage, not a TabbedPage. That's why the cast fails.

Looking at the code:

Line 177: var tabbedPage = (TabbedPage)Parent; - This assumes Parent is always a TabbedPage
Lines 160 and 170: The save/update buttons use await Navigation.PopAsync(); which is the correct way to go back
The cancel button should do the same - just pop the current page from navigation stack instead of trying to switch tabs.