---
title: "What are Type aliases in Kotlin?"
datePublished: Mon Apr 17 2023 21:24:35 GMT+0000 (Coordinated Universal Time)
cuid: clglcgfqp00000ammbcre1y40
slug: what-are-type-aliases-in-kotlin
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1681766508286/4820bb7e-eb6d-448b-a473-e75a12ddc765.png
tags: programming-blogs, android, kotlin, kotlin-beginner

---

Type alias in Kotlin is a feature that allows you to give a new name to an existing type. It can help make your code more readable and easier to understand.

Here's an example: let's say you're working on an Android app and you're using the type `Pair<String, Int>` a lot in your code. Instead of writing `Pair<String, Int>` every time you need to use it, you can create a type alias for it:

```kotlin
typealias StringIntPair = Pair<String, Int>
```

Now you can use the `StringIntPair` type alias instead of `Pair<String, Int>` in your code. Here's an example:

```kotlin
val pair: StringIntPair = "foo" to 42
```

This is the same as writing:

```kotlin
val pair: Pair<String, Int> = "foo" to 42
```

Type aliases can also be used with generic types, nullable types, and function types. For example, the following code defines a type alias for a nullable function that takes two integers as arguments and returns a nullable integer

```kotlin
typealias MyFunction = ((Int, Int) -> Int)?
```

Now you can use the type alias "MyFunction" instead of the function type `((Int, Int) -> Int)?`. For example, the following code creates a variable of type "MyFunction" and assigns a lambda expression to it:

```kotlin
val myFunction: MyFunction = { a, b -> a + b }
```

This is equivalent to creating a variable of the type `((Int, Int) -> Int)?` and assign a lambda expression to it:

```kotlin
val myFunction: ((Int, Int) -> Int)? = { a, b -> a + b }
```

You can have new names for `inner nested classes`

```kotlin
class A {
    inner class Inner
}
class B {
    inner class Inner
}

typealias AInner = A.Inner
typealias BInner = B.Inner
```

You can even use resource file names.

```kotlin
typealias Drawable = R.drawable
typealias Layout = R.layout

setContentView(Layout.activity_main)
imageView.setImageDrawable(ContextCompat.getDrawable(this,Drawable.ic_launcher_background))
```

In general, type aliases can make your code more concise and easier to read. They're especially useful when you're working with complex types or when you want to create your own custom types that are more specific to your app's needs.  
  
This is all about **typeAlias** in Koltin.

Happy learning.