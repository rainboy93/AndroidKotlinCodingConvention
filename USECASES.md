# Use Cases

## Table of Contents

- [Add new features module](#add-new-features-module)
- [UI](#ui)
- [Using ViewModel in right way](#using-viewmodel-in-right-way)
- [Image loading](#image-loading)
- [Dependency Injection](#dependency-injection)

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

       // SingleLiveEvent that is saved in the SavedState
      val singleLiveDataText by handle.singleLiveEvent<String?>()
  }
  ```

## Image loading

We use [Coil](https://coil-kt.github.io/coil) to display image. For more information, please go to [Coil Github page](https://coil-kt.github.io/coil)

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
