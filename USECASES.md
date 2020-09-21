# Use Cases

## Table of Contents

- [Add new features module](#add-new-features-module)
- [UI](#ui)
- [Dependency Injection](#dependency-injection)
- [Using ViewModel in right way](#using-viewmodel-in-right-way)
- [Image loading](#image-loading)

## UI

Always use the base UI class, ```vn.viettelpay.ui.BaseActivity``` and ```vn.viettelpay.ui.BaseFragment``` for fragment.

## Add new features module

There is a template feature module inside ```features``` group. To add a new module, just clone the module and follow below checklists:
- Change name of the new module, change the package name as well as package inside ```AndroidManifest.xml```, by now it is ```vn.viettelpay.template```.
  The package name should be ```vn.viettelpay.[feature_name]```
- Inside ```setting.gradle.kts```, include new module by adding ```"features:template"``` to the last line
- Inside ```BuildModules.kt```, add new variable in Features object like
  ```kotlin
  const val TEMPLATE = ":features:template"
  ```
- Inside ```build.gradle.kts``` of the ```app``` module, add ```BuildModules.Features.TEMPLATE``` in block ```dynamicFeatures```
- Sync the project

## Dependency Injection

We use [Koin](https://doc.insert-koin.io/) as Dependency Injection Framework.
One important note: For `Dynamic Feature Module`, we need to load Koin modules onCreate of Activity or Fragment before using it.

```kotlin
private val loadModules by lazy {
    loadKoinModules(myModule)
}

private fun injectFeatures = loadModules


class MyFragment: Fragment() {
    override fun onCreate() {
        ...
        injectFeatures()
        ...
    }
}
```

## Using ViewModel in right way

- Always inherit from ```vn.viettelpay.ui.BaseViewModel```
- Use Koin to inject ViewModel, note that ViewModel always has ```SavedStateHandle``` as first parameter
  ```kotlin
  viewModel { (handle: SavedStateHandle) -> MyStateVM(handle, get()) }
  ```
- Retrieve ViewModel in Activity 
  ```kotlin
  val myStateVM: MyStateVM by stateViewModel()
  ```
- To prevent data loss when system kill the app, use extension of ```SavedStateExtension.kt```

  ```kotlin
  // Define a ViewModel that takes a SavedStateHandle in argument
  class MainViewModel(handle: SavedStateHandle) : BaseViewModel() {
      // Simple string that is saved in the SavedState
      var manualText by handle.delegate<String?>()

      // MutableLiveData that is saved in the SavedState
      val liveDataText by handle.livedata<String?>()
  }
  ```

## Image loading

We use [Coil](https://coil-kt.github.io/coil) to display image. For more information, please go to [Coil Github page](https://coil-kt.github.io/coil)

## Animations

```kotlin
please {
   animate(avatar) toBe {
      bottomOfItsParent(marginDp = 36f)
      leftOfItsParent(marginDp = 16f)
      width(40, keepRatio = true, toDp = true)
   }
}.start()
```

- Follow scroll

Use `setPercent` to apply modify the current step of the animation

Exemple with a scrollview

```kotlin
val animation = please {
        animate(avatar) toBe {
           topOfItsParent(marginDp = 20f)
           leftOfItsParent(marginDp = 20f)
           scale(0.5f, 0.5f)
        }
}
scrollview.setOnScrollChangeListener(NestedScrollView.OnScrollChangeListener { v, scrollX, scrollY, oldScrollX, oldScrollY ->
    val percent = scrollY * 1f / v.maxScrollAmount
    animation.setPercent(percent)
})
```


- Chain animations

Just ask the kotlin's animation if he wants to execute another animation after, using `thenCouldYou animate`

```
please(duration = 1000L) {
   animate(image, withCameraDistance = 500f) toBe {
      flippedHorizontally()
   }
}.thenCouldYou(duration = 500L) {
   animate(image, withCameraDistance = 1000f) toBe {
      alpha(0.5f)
   }
}.start()
```

- Apply directly

If you want your animation to be applied directly, be bossy with kotlin and force it to apply it using `now()` !

```kotlin
please {
   animate(view) toBe {
      outOfScreen(Gravity.BOTTOM)
   }
}.now();
```

- Reset

Use `reset` to return to the initial state of views

```kotlin
animation.reset():
```

- List of expectations

```
please {
  animate(view) { //toBe is optional

     rightOf(view, marginDp=)
     leftOf(view, marginDp=)
     belowOf(view, marginDp=)
     aboveOf(view, marginDp=)

     originalPosition()

     sameCenterAs(view, horizontal=, vertical=)
     sameCenterHorizontalAs(view)
     sameCenterVerticalAs(view)
     centerInParent(horizontal=, vertical=)
     centerVerticalInParent()
     centerHorizontalInParent()

     centerBetweenViews(view1, view2, horizontal, vertical)
     centerBetweenViewAndParent(otherView, horizontal, vertical, toBeOnRight, toBeOnBottom)

     topOfItsParent()
     rightOfItsParent()
     bottomOfItsParent()
     leftOfItsParent()

     alignBottom(otherView, marginDp=)
     alignTop(otherView)
     alignLeft(otherView)
     alignRight(otherView)

     outOfScreen(gravitiy)  //Gravity.LEFT / Gravity.RIGHT / Gravity.TOP / Gravity.BOTTOM

     alpha(alpha)
     sameAlphaAs(otherView)
     visible()
     invisible()

     custom(object: CustomAnimExpectation(){ ... })

     originalScale()

     scale(scaleX, scaleY)
     height(height, keepRatio=, useDp=)
     width(width, keepRatio=, useDp=)
     sameScaleAs(otherView)
     sameWidthAs(otherView)
     sameHeightAs(otherView)

     marginTop(margin)
     marginBottom(margin)
     marginRight(margin)
     marginLeft(margin)

     paddingTop(padding)
     paddingBottom(padding)
     paddingRight(padding)
     paddingLeft(padding)

     textColor(textColor)
     textSize(textSize)
     backgroundAlpha(alpha)

     rotated(rotation)
     vertical(bottomOfViewAtLeft)
     atItsOriginalRotation()
}
````
