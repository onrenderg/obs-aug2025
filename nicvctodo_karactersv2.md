
\basic folder structure 
NICVC.Model

## Misc 
### skey
c+k, d = auto indent vs 
c + click = open defiantion file 
c+k c /u 

###

x 's 
x:Name
x:Class


###

# Logical character placemnt in file 
## Colors.xaml
## Styles.xaml
* TargetType="Label"
## xaml 
BackgroundColor
TextColor
"{AppThemeBinding Light={StaticResource MidnightBlue}, Dark={StaticResource White}}"
TextColor
"{AppThemeBinding Light=Black, Dark={StaticResource Black}}"
TextColor="Black" for selected items and TitleColor="Black" for placeholder

* Frame
	* BorderColor Margin  BackgroundColor VerticalOptions CornerRadius

* layout_hstack
<HorizontalStackLayout Grid.Row="3" HorizontalOptions="Center" Spacing="10"
 
## FillAndExpand port to Fill : 

Remove all stacklaout options use grid maui updated approach for xaml file such a way that it keeps layout same as now 
Refactor the page to use Grid (modern MAUI approach) while maintaining the same layout

# Structuer desctruing 
whenin open page what to key thing to look for copa work 

# Krash
All ObjectDisposedException issues resolved! The remaining Application.Current.MainPage assignments are appropriate for authentication state changes. 🎯

Now: Clean & Rebuild your solution to apply all changes! : 
Navigation.PopToRootAsync() or Navigation.PopAsync()):

## COncpets 

ListView vs CollectionView - Different events
ListView uses ItemTapped event with ItemTappedEventArgs
CollectionView uses SelectionChanged event with SelectionChangedEventArgs

```txt
CollectionView doesn't have ItemTapped - It's a ListView-only event
Different event args - ItemTappedEventArgs vs SelectionChangedEventArgs
Different data access - e.Item vs e.CurrentSelection[0]
Better UX - Need to clear selection to avoid stuck visual states
```


          <StackLayout  IsVisible="False">