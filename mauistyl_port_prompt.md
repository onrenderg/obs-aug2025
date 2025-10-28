Here's an optimized prompt for refactoring Xamarin.Forms XAML to modern .NET MAUI:

---

## **Prompt: Refactor Xamarin.Forms XAML to Modern .NET MAUI**

Refactor this XAML file from old Xamarin.Forms style to modern .NET MAUI. Follow these rules strictly:

### **Key Changes:**

1. **Navigation Header**
   - Replace: `<StackLayout Orientation="Horizontal">` with nested `<StackLayout Orientation="Vertical">`
   - With: `<HorizontalStackLayout>` with direct Label child
   - Remove unnecessary wrapper StackLayouts

2. **Deprecated Options - Replace:**
   - `FillAndExpand` → `Fill`
   - `CenterAndExpand` → `Center`
   - `StartAndExpand` → `Start`
   - `EndAndExpand` → `End`

3. **StackLayout Replacements:**
   - `<StackLayout Orientation="Horizontal">` → `<HorizontalStackLayout>`
   - `<StackLayout Orientation="Vertical">` or `<StackLayout>` → `<VerticalStackLayout>`
   - When replacing, update `<StackLayout.GestureRecognizers>` to `<VerticalStackLayout.GestureRecognizers>` or `<HorizontalStackLayout.GestureRecognizers>`

4. **Remove Unnecessary Wrappers:**
   - If a StackLayout contains only 1 child, remove it and place child directly
   - Example: Frame with StackLayout containing only Label → Frame with Label directly

5. **Grid Structure:**
   - Use `Grid RowDefinitions="Auto,*,Auto"` instead of nested wrapper StackLayouts
   - Remove StackLayout wrappers around Grids

6. **Frame Alignment:**
   - For horizontal content in Frame: Use `<HorizontalStackLayout HorizontalOptions="Center">` (not Fill)
   - Add `Padding="10"` to Frame instead of nested element padding

7. **Loading Overlay:**
   - Replace: `<ContentView Grid.RowSpan="999">` with nested StackLayouts
   - With: `<Grid Grid.Row="0" Grid.RowSpan="X">` where X = actual row count
   - Use `<HorizontalStackLayout>` for ActivityIndicator + Label

8. **Keep It Simple:**
   - Don't add unnecessary properties like `MinimumHeightRequest` unless required
   - Don't change working functionality
   - Use `Spacing` property instead of individual Margins

### **Example Pattern:**

**Before:**
```xml
<StackLayout Orientation="Horizontal" HorizontalOptions="FillAndExpand">
    <Label HorizontalOptions="FillAndExpand"/>
    <Image HorizontalOptions="End"/>
</StackLayout>
```

**After:**
```xml
<HorizontalStackLayout HorizontalOptions="Center" Spacing="10">
    <Label/>
    <Image/>
</HorizontalStackLayout>
```

Now refactor the provided XAML file following these rules exactly.

---

**This prompt is concise, specific, and includes the exact patterns you need!**