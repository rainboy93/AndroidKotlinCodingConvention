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
