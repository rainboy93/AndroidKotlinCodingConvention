# Use Cases

## Table of Contents

- [Add new features module](#add-new-features-module)
- [Image loading](#image_loading)

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
