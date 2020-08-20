# Use Cases

## Table of Contents

- [Add new features module](#add-new-features-module)
- [Image loading](#image_loading)
- [Using ViewModel in right way](#using-viewmodel-in-right-way)

## Add new features module

There is a template feature module inside ```features``` group. To add a new module, just clone the module and follow below checklists:
- Change name of the new module, change the package name as well as package inside ```AndroidManifest.xml```, by now it is ```vn.viettelpay.template```
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
