# Android Kotlin Coding Convention

## Table of Contents

- [Nomenclature](#nomenclature)
  + [Packages](#packages)
  + [Classes & Interfaces](#classes--interfaces)
  + [Methods](#methods)
  + [Fields](#fields)
  + [Variables & Parameters](#variables--parameters)
  + [Misc](#misc)
- [Declarations](#declarations)
  + [Visibility Modifiers](#visibility-modifiers)
  + [Fields & Variables](#fields--variables)
  + [Classes](#classes)
  + [Data Type Objects](#data-type-objects)
  + [Enum Classes](#enum-classes)
- [Spacing](#spacing)
  + [Indentation](#indentation)
  + [Line Length](#line-length)
  + [Vertical Spacing](#vertical-spacing)
- [Coding Rules](#coding-rules)
  + [Semicolons](#semicolons)
  + [Getters & Setters](#getters--setters)
  + [Brace Style](#brace-style)
  + [When Statements](#when-statements)
  + [Use an IDE suggestion](#use-an-ide-suggestion)
  + [Use a smart cast](#use-a-smart-cast)
  + [`it` in Lambda expression applies to wide scope](#it-in-lambda-expression-applies-to-wide-scope)
  + [Should use a type interface](#should-use-a-type-interface)
  + [Don't write for loop](#dont-write-for-loop)
  + [Use `to` expression creating `Pair` class](#use-to-expression-creating-pair-class)
  + [Use `when` in case there are two or more branches of `if-else`](#use-when-in-case-there-are-two-or-more-branches-of-if-else)
  + [Use `is` in case of comparing a class type](#use-is-in-case-of-comparing-a-class-type)
  + [Use `range` in case comparing Int values](#use-range-in-case-comparing-int-values)
  + [Don't start a new line in variable declaration using `if-else`](#dont-start-a-new-line-in-variable-declaration-using-if-else)
- [Scope function](#scope-function)
  + [Should use scope function](#should-use-scope-function)
  + [Don't declare variables that used only once](#dont-declare-variables-that-used-only-once)
  + [which use `run` or `let`](#which-use-run-or-let)
- [Function](#function)
  + [Omit a type of return value](#omit-a-type-of-return-value)
  + [Don't name `setHoge`, `getHoge`](#dont-name-sethoge-gethoge)
  + [Use named arguments for function overloading](#use-named-arguments-for-function-overloading)
  + [Use typealias](#use-typealias)
  + [Extension functions](#extension-functions)
  + [Private extension functions](#private-extension-functions)
  + [Don't create extension functions in same class](#dont-create-extension-functions-in-same-class)
- [Types](#types)
  + [Type Inference](#type-inference)
  + [Constants vs. Variables](#constants-vs-variables)
  + [Companion Objects](#companion-objects)
  + [Nullable Types](#nullable-types)
- [XML Guidance](#xml-guidance)
  + [XML File Names](#xml-file-names)
  + [Indentation](#indentation-1)
  + [Use Context-Specific XML Files](#use-context-specific-xml-files)
  + [XML Attribute Ordering](#xml-attribute-ordering)
  + [View IDs](#view-ids)
- [Language](#language)

## Nomenclature

On the whole, naming should follow Java standards, as Kotlin is a JVM-compatible language.

### Packages

Package names are similar to Java: all __lower-case__, multiple words concatenated together, without hypens or underscores:

__BAD__:

```kotlin
vn.ViettelPay.network
```

__GOOD__:

```kotlin
vn.viettelpay.network
```

### Classes & Interfaces

Written in __UpperCamelCase__. For example `BaseCallAdapter`. 

### Methods

Written in __lowerCamelCase__. For example `setValue`.

### Fields

Generally, written in __lowerCamelCase__. Fields should **not** be named with Hungarian notation, as Hungarian notation is [erroneously thought](http://jakewharton.com/just-say-no-to-hungarian-notation/) to be recommended by Google.

Example field names:

```kotlin
class MyClass {
  var publicField: Int = 0
  val person = Person()
  private var privateField: Int?
}
```

Constant values in the companion object should be written in __uppercase__, with an underscore separating words:

```kotlin
companion object {
  const val THE_ANSWER = 42
}
```

### Variables & Parameters

Written in __lowerCamelCase__.

Single character values must be avoided, except for temporary looping variables.

Abbreviations in variable names are strongly discouraged. Acronyms may be used if they are standard nomenclature (commonly used in place of their longhand counterparts).

__BAD:__

```kotlin
val bookTtl = "Programming 101"
val ipAddr = "127.0.0.1"
```
__GOOD:__

```kotlin
val bookTitle = "Programming 101"
val ipAddress = "127.0.0.1"
```

Boolean Feature Flags configured remotely should be named such that true coresponds to the feature being enabled and false is disabled.

__BAD:__

```kotlin
val featureAbc = ExampleRemoteBoolean("feature_abc_disabled", true)  // WRONG! true would result in feature being enabled
```
__GOOD:__

```kotlin
val featureAbc = ExampleRemoteBoolean("feature_abc", true) // Okay, defaults to enabled
val featureAbc = ExampleRemoteBoolean("feature_abc", false) // Okay, defaults to disabled
```

### Misc

In code, acronyms should be treated as words. For example:

__BAD:__

```kotlin
XMLHTTPRequest
URL: String? 
findPostByID
```
__GOOD:__

```kotlin
XmlHttpRequest
url: String
findPostById
```

## Declarations

### Visibility Modifiers

Only include visibility modifiers if you need something other than the default of public.

**BAD:**

```kotlin
public val wideOpenProperty = 1
private val myOwnPrivateProperty = "private"
```

**GOOD:**

```kotlin
val wideOpenProperty = 1
private val myOwnPrivateProperty = "private"
```

### Access Level Modifiers

Access level modifiers should be explicitly defined for classes, methods and member variables.

### Fields & Variables

Prefer single declaration per line.

__GOOD:__

```kotlin
username: String
twitterHandle: String
```

### Classes

Exactly one class per source file, although inner classes are encouraged where scoping appropriate.

### Data Type Objects

Prefer data classes for simple data holding objects.

__BAD:__

```kotlin
class Person(val name: String) {
  override fun toString() : String {
    return "Person(name=$name)"
  }
}
```

__GOOD:__

```kotlin
data class Person(val name: String)
```

### Enum Classes

Enum classes without methods may be formatted without line-breaks, as follows:

```kotlin
enum class AccountStatus { ACTIVE, LOCK_WRONG_PIN, LOCK_BY_CUSTOMER, CANCEL; }
```

## Spacing

Spacing is especially important in coding, as code needs to be easily readable as part of the tutorial. 

### Indentation

Indentation is using spaces - never tabs.

#### Blocks

Indentation for blocks uses 2 spaces:

__BAD:__

```kotlin
for (i in 0..9) {
    Log.i(TAG, "index=" + i)
}
```

__GOOD:__

```kotlin
for (i in 0..9) {
  Log.i(TAG, "index=" + i)
}
```

#### Line Wraps

Indentation for line wraps should use 4 spaces:

__BAD:__

```kotlin
val widget: CoolUiWidget =
        someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line)
```

__GOOD:__

```kotlin
val widget: CoolUiWidget =
    someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line)
```

### Line Length

Lines should be no longer than 100 characters long.


### Vertical Spacing

There should be exactly one blank line between methods to aid in visual clarity and organization. Whitespace within methods should separate functionality, but having too many sections in a method often means you should refactor into several methods.

## Comments

When they are needed, use comments to explain **why** a particular piece of code does something. Comments must be kept up-to-date or deleted.

Avoid block comments inline with code, as the code should be as self-documenting as possible. *Exception: This does not apply to those comments used to generate documentation.*

## Coding Rules

### Semicolons

Semicolons ~~are dead to us~~ should be avoided wherever possible in Kotlin. 

__BAD__:

```kotlin
val horseGiftedByTrojans = true;
if (horseGiftedByTrojans) {
  bringHorseIntoWalledCity();
}
```

__GOOD__:

```kotlin
val horseGiftedByTrojans = true
if (horseGiftedByTrojans) {
  bringHorseIntoWalledCity()
}
```

### Getters & Setters

Unlike Java, direct access to fields in Kotlin is preferred. 

If custom getters and setters are required, they should be declared [following Kotlin conventions](https://kotlinlang.org/docs/reference/properties.html) rather than as separate methods.

### Brace Style

Only trailing closing-braces are awarded their own line. All others appear the same line as preceding code:

__BAD:__

```kotlin
class MyClass
{
  fun doSomething()
  {
    if (someTest)
    {
      // ...
    }
    else
    {
      // ...
    }
  }
}
```

__GOOD:__

```kotlin
class MyClass {
  fun doSomething() {
    if (someTest) {
      // ...
    } else {
      // ...
    }
  }
}
```

Conditional statements are always required to be enclosed with braces, irrespective of the number of lines required.

__BAD:__

```kotlin
if (someTest)
  doSomething()
if (someTest) doSomethingElse()
```

__GOOD:__

```kotlin
if (someTest) {
  doSomething()
}
if (someTest) { doSomethingElse() }
```

### When Statements

Unlike `switch` statements in Java, `when` statements do not fall through. Separate cases using commas if they should be handled the same way. Always include the else case.

__BAD:__

```kotlin
when (anInput) {
  1 -> doSomethingForCaseOneOrTwo()
  2 -> doSomethingForCaseOneOrTwo()
  3 -> doSomethingForCaseThree()
}
```

__GOOD:__

```kotlin
when (anInput) {
  1, 2 -> doSomethingForCaseOneOrTwo()
  3 -> doSomethingForCaseThree()
  else -> println("No case satisfied")
}
```
### Idiom

#### Use an IDE suggestion

```kotlin
val array = ArrayList<Int>()
```

__BAD:__
```kotlin
array.get(0)    

getActivity().finish()
```

__GOOD:__
```kotlin
array[0]

requireActivity().finish()
```

#### Use a smart cast

```kotlin
fun hoge(value: Boolean?) {
    value ?: return
    if (value) {

    }
}

fun hoge(context: Context) {
    context as Activity
    context.finish() // finish activity
}
```

__BAD:__
```kotlin
if (hoge !is Hoge) {
    throw IllegalArgumentException("not Hoge!")
}
hoge.foo()
```

__GOOD:__
```kotlin
hoge as? Hoge ?: throw IllegalArgumentException("not Hoge!")
hoge.foo()
```

#### `it` in Lambda expression applies to wide scope

__BAD:__
```kotlin
// bad
{ hoge -> 
  hoge?.let { it.foo() }
}
```

__GOOD:__
```kotlin
{ 
  it?.let { hoge -> hoge.foo() }
}
```

#### Should use a type interface

You can write a type if it is difficult to understand.

* property

```kotlin
val hoge = 0  // Int
val foo = 10L // Long
val bar = 100f //Float
```

* function

```Kotlin
// return Boolean
fun Context.isConnectToWifi() =
      (getSystemService(Context.CONNECTIVITY_SERVICE) as ConnectivityManager)
         .activeNetworkInfo?.type == ConnectivityManager.TYPE_WIFI

// return Point
fun Display.getSize(): Point = Point().apply { getSize(this) }
```

#### Don't write for loop

You don't have to write for loop because threre is `forEach` in collections package of Kotlin.

__BAD:__
```kotlin
for (i in 0..9) {
}
```

__GOOD:__
```kotlin
(0..9).forEach {
}

(0..9).forEachIndexed { index, value ->
}
```

#### Use `to` expression creating `Pair` class

__BAD:__
```kotlin
val pair = Pair(foo, bar) 
```

__GOOD:__
```kotlin
val pair = foo to bar
```

* `to` is infix function

```kotlin public infix fun <A, B> A.to(that: B): Pair<A, B> = Pair(this, that)```

#### Use `range`

```kotlin
val char = 'K'
```

__BAD:__
```kotlin
if (char >= 'A' && 'c' <= 'Z') print("Hit!")
```

__GOOD:__
```kotlin
if (char in 'A'..'Z') print("Hit!")

when (char) {
   in 'A'..'Z' -> print("Hit!")
   else -> return
}
```

#### Use `when` in case there are two or more branches of if-else

__BAD:__
```kotlin
val hoge = 10if (hoge > 10) {

} else if (hoge > 5) {

} else if (hoge > 0) {

} else {

}
```

__GOOD:__
```kotlin
when {
    hoge > 10 -> print("10")
    hoge > 5 -> print("0")
    hoge > 0 -> print("0")
    else -> print("else")
}
```

#### Use `is` in case of comparing a class type

```kotlin
val hoge: Hoge = Hoge()
when (hoge) {
    is Hoge -> {

    }
    else -> {
       
    }
}
```

#### Use `range` in case comparing Int values

```kotlin
val hoge = 10
when (hoge) {
    in 0..4 -> print("0..4")
    in 5..10 -> print("5..10")
}
```

#### Don't start a new line in variable declaration using if-else 

```kotlin
val foo: Int = 5
```

__BAD:__
```kotlin
val bar = if (foo > 10) {
    "kotlin"
} else {
    "java"
}
```

__GOOD:__
```kotlin
val bar = if(foo > 10) "kotlin" else "java"
```

## Scope function

### Should use scope function

```kotlin
class Hoge {
    fun fun1() {}
    fun fun2() {}
}
```

__BAD:__
```kotlin
val hoge = Hoge()
hoge.fun1()
hoge.fun2()
```

__GOOD:__
```kotlin
val hoge = Hoge().apply {
   fun1()
   fun2()
}
```

You don't need to use `with` because you can substitute `run`, `let`, `apply`, `also`.

### Don't declare variables that used only once

You can express using a scope function.  
But it becomes hard to read in case it excessibely use.  
You should declare variables if you need to think.

```kotlin
class Foo

class Bar(val foo: Foo)

class Hoge {
    fun fun1() {}
    fun fun2(bar: Bar) {}
    fun fun3(foo: Foo) {}
}
```

__BAD:__
```kotlin
val hoge = Hoge()
val foo = Foo()
val bar = Bar(foo)
hoge.fun1()
hoge.fun2(bar)
hoge.fun3(foo)
```

__GOOD:__
```kotlin
Hoge().run {    
   fun1()
   Foo().let {        
       fun2(Bar(it))
       fun3(it)
   }
}
```

### which use `run` or `let`

* Use `let` to substitute into functions
* Use `run` to use outside functions

```kotlin
class Foo

class Bar(val foo: Foo)

class Hoge {
    fun fun1() {}
    fun fun2(bar: Bar) {}
    fun fun3(foo: Foo) {}
}
```

__BAD:__
```kotlin
Hoge().let {
   it.fun1()
   Foo().run {
       it.fun2(Bar(this))
       it.fun3(this)
   }
}
```

__GOOD:__
```kotlin
Hoge().run {    
   fun1()
   Foo().let {        
       fun2(Bar(it))
       fun3(it)
   }
}
```

## Types 

Always use Kotlin's native types when available. Kotlin is JVM-compatible so **[TODO: more info]**

### Type Inference

Type inference should be preferred where possible to explicitly declared types. 

__BAD:__

```kotlin
val something: MyType = MyType()
val meaningOfLife: Int = 42
```

__GOOD:__

```kotlin
val something = MyType()
val meaningOfLife = 42
```

### Constants vs. Variables 

Constants are defined using the `val` keyword, and variables with the `var` keyword. Always use `val` instead of `var` if the value of the variable will not change.

*Tip*: A good technique is to define everything using `val` and only change it to `var` if the compiler complains!

### Companion Objects

** TODO: A bunch of stuff about companion objects **

### Nullable Types

Declare variables and function return types as nullable with `?` where a `null` value is acceptable.

Use implicitly unwrapped types declared with `!!` only for instance variables that you know will be initialized before use, such as subviews that will be set up in `onCreate` for an Activity or `onCreateView` for a Fragment.

When naming nullable variables and parameters, avoid naming them like `nullableString` or `maybeView` since their nullability is already in the type declaration.

When accessing a nullable value, use the safe call operator if the value is only accessed once or if there are many nullables in the chain:

```kotlin
editText?.setText("foo")
```

#### Don't use `!!`

Don't use `!!`, it will erase the benefits of Kotlin.  
You use it only when you want to explicitly raise a Null Pointer Exception.

#### Use a scope function in case of checking a null value

```Kotlin
class Hoge {
    fun fun1() {}
    fun fun2() {}
    fun fun3() = true
}

var hoge: Hoge? = null

// not good
if (hoge != null) {
    hoge.fun1()
} else {
    val hoge = Hoge()
    hoge.fun1()
    hoge.fun2()
}

// good
hoge?.run { 
   fun1()
} ?: run {
    hoge = Hoge().apply {
        fun1()
        fun2()
    }
}

// good
if (hoge != null && hoge.fun3()) {
    hoge.fun1()
} else {
    hoge = Hoge().apply {
       fun1()
       fun2()
    }
}
```

## Function

### Omit a type of return value

Basically, we omit a type of return value as declaration variables using type interface.  
You should write it in case we cannot guess from a method name.  

```kotlin
fun createIntent(context: Context, foo: Int, bar: Boolean) = 
Intent(context, HogeActivity::class.java).apply {    
   putExtra("foo", foo)
   putExtra("bar", bar)
}

fun hoge(value: Int): String = when (value) {
   in 0..10 -> "foo"
   in 100..500 -> "bar"
   else -> "else"
}
```


### Don't name `setHoge`, `getHoge`

Don't name `setHoge`, `getHoge` at property and function because it is used in Kotlin language.

__BAD:__
```kotlin
fun setHoge() {
}
```

### Use named arguments for function overloading

__BAD:__
```kotlin
class Hoge {
   fun hoge() {
      print("hoge")
   }

   fun hoge(prefix: String) {
       print(prefix + "hoge")
   }
}
```

__GOOD:__
```kotlin
class Hoge {
   fun hoge(prefix: String = "") {
      print(prefix + "hoge")
   }
}
```

### Use typealias

__BAD:__
```kotlin
interface CallBackListener {
   fun onHoge(foo: String, bar: Int)
}

// caller
var callback: CallBackListener? = null
callback?.onHoge("foo", 100)

// callee
val callback = object : CallBackListener {
  override fun onHoge(foo: String, bar: Int) {
    print("$foo : $bar")
  }
}
```

__GOOD:__
```kotlin
typealias CallBackListener = (foo: String, bar: Int) -> Unit

// caller
var callback: CallBackListener? = null
callback?.invoke("foo", 100)

// callee
val callback = { foo, bar -> 
  print("$foo : $bar")
}
```

### Extension functions

* Use it as utility functions in Java
* It is not necessary to use extension functions in case it is defined wide scope.
 i.g. String
 In case we recommend the private extension functions.

* Extension class name : `HogeExt.kt`

* Structure of package 

```
main
 |-data
 |-ui
   |-util
     |-ext
 |-util
   |-ext
```

### Private extension functions

Functions taking only one object as an argument replace private extension functions. (not necessary)

```kotlin
enum class Hoge() {
    FOO,
    BAR,
    NONE
}
```

__BAD:__
```kotlin
fun toHoge(arg: String): Hoge {
    if (!arg.startsWith("hoge")) {
        return Hoge.NONE    
    }
    return when (arg) {
       "hogeFoo" -> Hoge.FOO
       "hogeBar" -> Hoge.BAR
       else -> Hoge.NONE
    }
}
```

__GOOD:__
```kotlin
fun String.toHoge(): Hoge {
    if (!startsWith("hoge")) {
        return Hoge.NONE    
    }
    return when (this) {
       "hogeFoo" -> Hoge.FOO
       "hogeBar" -> Hoge.BAR
       else -> Hoge.NONE    }
    }
}
```

### Don't create extension functions in same class.

```kotlin
class Hoge {

   // bad
   fun Hoge.foo() {
   }

   // good
   fun foo() {
   }
}
```

## XML Guidance

Since Android uses XML extensively in addition to Java, we have some rules
specific to XML.

### XML File Names

View-based XML files should be prefixed with the type of view that they
represent.

__BAD:__

- `login.xml`
- `main_screen.xml`
- `rounded_edges_button.xml`

__GOOD:__

- `activity_login.xml`
- `fragment_main_screen.xml`
- `button_rounded_edges.xml`

If the XML files is store in local modules, it should be prefixed with module name.

__GOOD:__

- `commons_button_gradient.xml`
- `commons_fragment_base.xml`

### Indentation

Similarly to Kotlin, indentation should be __two characters__.

### Use Context-Specific XML Files

Wherever possible XML resource files should be used:

- Strings => `res/values/strings.xml`
- Styles => `res/values/styles.xml`
- Colors => `res/color/colors.xml`
- Animations => `res/anim/`
- Drawable => `res/drawable`


### XML Attribute Ordering

Where appropriate, XML attributes should appear in the following order:

- `id` attribute
- `layout_*` attributes
- style attributes such as `gravity` or `textColor`
- value attributes such as `text` or `src`

Within each of these groups, the attributes should be ordered alphabetically.

### View IDs

When Kotlin extensions are used (and view IDs are made available via import), view ID names (android:id in XML) should be all lowercase with underscores separating words (snake_case). It is required that every name have at least one underscore to distinguish it from local variables. In instances were it proves difficult, then name may be postfixed with the component type (e.g. _button or _view).

__BAD:__

```xml
<android.support.v7.widget.RecyclerView
    android:id="@+id/moves"
    />
```

```xml
<android.support.v7.widget.RecyclerView
    android:id="@+id/danceMoves"
    />
```

__GOOD:__

```xml
<android.support.v7.widget.RecyclerView
    android:id="@+id/dance_moves"
    />
```

## Language

Use `en-US` English spelling. 🇺🇸

__BAD:__

```kotlin
val colourName = "red"
```

__GOOD:__

```kotlin
val colorName = "red"
```
