
```xml
    <NavigationPage.TitleView>

        <!-- <StackLayout    x:Name="Custom_Navigation"

                    Orientation="Horizontal"

                    HorizontalOptions="FillAndExpand"

                    VerticalOptions="CenterAndExpand"

                    BackgroundColor="Transparent" >

            <Image  Source="goi_icon.png"

                    HeightRequest="40"

                    VerticalOptions="CenterAndExpand"/>

            <Label  x:Name="Lbl_Nav_title"

                    Style="{StaticResource NavBar_LabelStyle}" />

            <Image  Source="app_nic_header.png"

                    x:Name="Image_Nav_nic"

                    HeightRequest="30"

                    VerticalOptions="CenterAndExpand"/>

        </StackLayout> -->

        <Grid   x:Name="Custom_Navigation"

                HorizontalOptions="Fill"

                VerticalOptions="Center">

            <Label  x:Name="Lbl_Nav_title"

                    Style="{StaticResource NavBar_LabelStyle}"

                    HorizontalTextAlignment="Center"

                    VerticalTextAlignment="Center"

                    HorizontalOptions="Center"

                    VerticalOptions="Center"/>

            <Image  Source="app_nic_header.png"

                    x:Name="Image_Nav_nic"

                    HeightRequest="30"

                    HorizontalOptions="Start"

                    VerticalOptions="Center"

                    Margin="11,0,0,0"/>

        </Grid>

    </NavigationPage.TitleView>

```






## UI representation (ASCII layout)
+--------------------------------------------------------------+
|                       [ Title Bar ]                          |
|  ┌────────────────────────────────────────────────────────┐  |
|  | [🖼️ ic_launcher.png]     NIC Video Conferencing        |  |
|  |   ↑ (Start-aligned)       ↑ (Centered Label)            |  |
|  └────────────────────────────────────────────────────────┘  |
+--------------------------------------------------------------+





## in App.xaml  or Styles.xaml
<Style x:Key="NavBar_LabelStyle" TargetType="Label">
	<Setter Property="FontSize" Value="2"/> 

## Style xaml key Usage in xaml file


<Label  x:Name="Lbl_Nav_title"
    Style="{StaticResource 
    	}"



# attributes are placed on new lines
Shift  + altf  

## Code folding 
            <Setter Property="FontSize"
                    Value="18"/>