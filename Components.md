# Buttons

There are two types of buttons ```CoreButtonType.GRADIENT``` and ```CoreButtonType.OUTLINE```, three types of button size ```CoreButtonSize.SMALL```, ```CoreButtonSize.MEDIUM```, and ```CoreButtonSize.LARGE```

## Attributes:
- ```cbtText``` String or resource id text for button
- ```cbtSize``` Define button size ```small, medium, large```
- ```cbtType``` Define button type ```gradient, outline```

## Sample code 
```kotlin
// Gradient small
<vn.viettelpay.views.button.CoreButton
        android:id="@+id/buttonSmall"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        app:cbtSize="small"
        app:cbtText="Button Small"
        app:cbtType="gradient"/>
// Outline medium
<vn.viettelpay.views.button.CoreButton
        android:id="@+id/buttonSmall"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        app:cbtSize="medium"
        app:cbtText="Button Small"
        app:cbtType="outline"/>
```

# Inputs

## CoreInputField
Input field for various type of purposes

### Attributes:
- ```cifText``` Input field text value
- ```cifHint``` String or resource id hint of input field
- ```cifHeader``` String or resource id header of input field, if empty header will take value of hint
- ```cifWarning``` String or resource id warning of input field
- ```cifInputType``` Define type of input field ```baseline, secure, money, contacts, date, card, text_area, choose```

Sample code:
```kotlin
<vn.viettelpay.views.input.CoreInputField
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      app:cifHeader="@string/app_name"
      app:cifHint="@string/app_name"
      app:cifInputType="choose"
      app:cifText="@string/app_name"
      app:cifWarning="@string/app_name" />
```

## AuthenticationInputField
Input field for Authentication screens

### Attributes:
- ```aifText``` Input field text value
- ```aifHint``` String or resource id hint of input field
- ```aifHeader``` String or resource id header of input field, if empty header will take value of hint
- ```aifWarning``` String or resource id warning of input field
- ```aifInputType``` Define type of input field ```phone, password```
- ```aifAlwaysShowKeyboard``` Should prevent keyboard from dismissing when has focus

### Sample code:
```kotlin
<vn.viettelpay.views.input.AuthenticationInputField
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      app:aifHeader="@string/app_name"
      app:aifHint="@string/app_name"
      app:aifInputType="phone"
      app:aifText="@string/app_name"
      app:aifWarning="@string/app_name" />
```

### PinInputField
Input field for passcode screeen

### Attributes
- ```pifHeader``` String or resource id header

### Sample code
```kotlin
<vn.viettelpay.views.input.PinInputField
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      app:pifHeader="@string/app_name"/>
```

To get value from input field use ```values()``` function.
To retrieve input field use public variable ```inputField```.

# Divider

The default divider is configured using the values of the theme attributes and it can be attached to a ```RecyclerView``` in Kotlin with:
```kotlin
// Using LinearLayoutManager or GridLayoutManager.
recyclerView.addDivider()
// Using StaggeredGridLayoutManager.
recyclerView.addStaggeredDivider()
```

## Theme attributes
By default, all the dividers can be customized with these theme attributes:

- ```android:listDivider``` or ```recyclerViewDividerDrawable``` → the divider's Drawable or color
- ```recyclerViewDividerSize``` → the divider's size (otherwise it would be inherited by the Drawable)
- ```recyclerViewDividerInsetStart``` → the start inset of the divider's Drawable (otherwise 0)
- ```recyclerViewDividerInsetEnd``` → the end inset of the divider's Drawable (otherwise 0)
- ```recyclerViewDividerTint``` → the tint of the divider's Drawable (otherwise the Drawable won't be tinted)
- ```recyclerViewDividerAsSpace``` → true if the divider will behave as a simple space, without drawing anything (by default it's false)

## Programmatic configuration
Each divider can be customized programmatically using the classes ```DividerBuilder``` and ```StaggeredDividerBuilder```. The properties of a divider specified programmatically win over the theme attributes.
Using ```LinearLayoutManager``` and ```GridLayoutManager```, the correct builder class is DividerBuilder which can be instantiated in Kotlin with:
```kotlin
context.dividerBuilder()
.....
.build()
.addTo(recyclerView)
```
Using ```StaggeredGridLayoutManager```, the correct builder class is ```StaggeredDividerBuilder``` which can be instantiated in Kotlin with:
```kotlin
context.staggeredDividerBuilder()
.....
.build()
.addTo(recyclerView)
```