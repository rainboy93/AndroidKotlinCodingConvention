# NavigationBar

## Attributes:
- ```nbHeader``` String resource or raw string of this navigation bar title
- ```nbBackType``` To change left button drawable based on types ```none, back, close```

To set up a NavigationBar with Activity simply call
```kotlin
/**
   * Initialize functions for NavigationBar
   * @param activity activity context
   * @param action action list of this NavigationBar
   */
  fun setUpNavigationBar(activity: Activity, vararg action: NavigationBarAction)
```

To receive callback when user tap the NavigationBar actions, assign a listener to
```kotlin
var actionListener: NavigationBarActionListener? = null
```

## Sample code 
```xml
 <vn.viettelpay.views.navigation.VDSNavigationBar
      android:id="@+id/navigationBar"
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      app:nbBackType="none"
      app:nbHeader="Navigation bar" />
```

# CardView

## Attributes:
- ```cvType``` Define card shadow types ```basic, custom```
- ```cvShadowStartColor``` Shadow start color of CardView
- ```cvShadowEndColor``` Shadow end color of CardView
- ```cvBackgroundColor``` Background color for CardView
- ```cvCornerRadius``` Corner radius for CardView
- ```cvElevation``` Elevation for CardView
- ```cvMaxElevation``` Maximum Elevation for CardView
- ```cvUseCompatPadding``` Add padding in API v21+ as well to have the same measurements with previous versions
- ```cvPreventCornerOverlap``` Add padding to CardView on v20 and before to prevent intersections between the Card content and rounded corners
- ```cvContentPadding``` Inner padding between the edges of the Card and children of the CardView
- ```cvContentPaddingLeft``` Inner padding between the left edge of the Card and children of the CardView
- ```cvContentPaddingRight``` Inner padding between the right edge of the Card and children of the CardView
- ```cvContentPaddingTop``` Inner padding between the top edge of the Card and children of the CardView
- ```cvContentPaddingBottom``` Inner padding between the bottom edge of the Card and children of the CardView
- ```android:minWidth``` Workaround to read user defined minimum width
- ```android:minHeight``` Workaround to read user defined minimum height

## Sample code 
```xml
 <vn.viettelpay.views.cardview.VDSCardView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:cvBackgroundColor="@color/tokenWhite"
        app:cvCornerRadius="@dimen/tokenBorderRadius08"
        app:cvPreventCornerOverlap="false">

        <vn.viettelpay.views.VDSTextView
          style="@style/fontBold32"
          android:layout_width="match_parent"
          android:layout_height="@dimen/_100sdp"
          android:gravity="center"
          android:text="Card"
          android:textColor="@color/tokenCyan100"
          tools:ignore="HardcodedText" />
      </vn.viettelpay.views.cardview.VDSCardView>
```

# RadioButton

## Attributes:
- ```rbText``` String resource id for button

## Sample code 
```kotlin
 <RadioGroup
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <vn.viettelpay.views.VDSRadioButton
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_margin="@dimen/tokenSpacing16"
          app:rbText="@string/app_name" />

        <vn.viettelpay.views.VDSRadioButton
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_margin="@dimen/tokenSpacing16"
          app:rbText="@string/app_name"  />
 </RadioGroup>
```

# CheckBox

## Attributes:
- ```cbText``` String resource id for CheckBox

## Sample code 
```kotlin
 <vn.viettelpay.views.VDSCheckBox
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_margin="@dimen/tokenSpacing16"
        app:cbText="@string/app_name" />
```

# Badge

## Attributes:
- ```bType``` Define badge color type ```red, cyan, green, yellow```

## Sample code 
```kotlin
<vn.viettelpay.views.VDSBadge
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:text="99"
      app:bType="red" />
```

# TextView

## Attributes:
- ```tvText``` String resource id for TextView
- ```tvPreventFastClick``` Prevent clicking too fast
- ```tvEnableClickEffect``` DefineAlpha pressed effect
- ```tvEnableAutoScroll``` Auto scroll for long horizontal text

## Sample code 
```kotlin
<vn.viettelpay.views.VDSTextView
      android:id="@+id/inputTitle"
      style="@style/fontBold16"
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:layout_marginStart="@dimen/tokenSpacing16"
      android:textColor="@color/tokenBlue100"
      app:layout_constraintBottom_toBottomOf="@+id/buttonShowError"
      app:layout_constraintStart_toStartOf="parent"
      app:layout_constraintTop_toTopOf="@+id/buttonShowError"
      app:tvEnableAutoScroll="true"
      app:tvEnableClickEffect="true"
      app:tvPreventFastClick="true"
      app:tvText="@string/app_name" />
```

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
