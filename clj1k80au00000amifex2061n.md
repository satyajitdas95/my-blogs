---
title: "Essential Data Structures for your upcoming Android interview - Part 1"
seoTitle: "Crucial Android Interview Data Structures"
seoDescription: "Master essential data structures for Android interviews and development, including arrays, lists, hashmaps, sets, queues, stacks, trees, and graphs. Enhance"
datePublished: Sun Jun 18 2023 15:05:42 GMT+0000 (Coordinated Universal Time)
cuid: clj1k80au00000amifex2061n
slug: essential-data-structures-for-your-upcoming-android-interview-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1682019517181/c0e26a09-c088-4c9b-ae2f-3a65089e9b67.png
tags: android-development, data-structures, android, kotlin, data-structure-and-algorithms

---

The first round of an Android interview focusing on DSA helps employers assess a candidate's foundational knowledge, problem-solving abilities, and potential for developing efficient and scalable Android applications.

It is a crucial step in identifying candidates who can handle complex programming challenges and contribute effectively to the development team.

---

Data structures are a fundamental concept in computer science that allow us to store and organize data efficiently and effectively.

In the world of Android development, understanding the different types of data structures and how to use them can make a significant difference in the **performance** and **functionality** of your application.

In this blog, we will explore some of the most commonly used data structures by Android developers and how they can be implemented in your own projects.

Whether you are a beginner or an experienced developer, this guide will provide you with a solid foundation in the world of data structures for Android development.

Though there are numerous concepts to grasp, we will concentrate solely on those most commonly utilized from an Android perspective.

In this blog, we will cover these data structures.

`Array` `List` `HashMap` `Sets` `Queue` `Stack` `Tree` `Graph`

Before delving into the data structures, let's discuss where they are stored: the RAM.

## What is RAM?

Certainly! RAM, or Random Access Memory, is a vital part of a computer's hardware. It is responsible for temporarily storing data and instructions actively used by the computer's processor.

From a data structure perspective, RAM can be thought of as a large collection of storage cells, each capable of storing a certain amount of information. These cells are organized into a two-dimensional grid of bits. A bit is the smallest unit of data in a computer, representing a binary value of either 0 or 1.

The size of RAM is typically measured in terms of bytes. A byte consists of 8 bits. So, when you see specifications like 4 GB (gigabytes) of RAM, it means there are approximately 4 billion bytes of storage available.

Now, let's understand how data structures utilize RAM. When you create variables, arrays, or other data structures in a programming language, they occupy a certain amount of memory in RAM based on their data type and size.

For example, let's consider an integer variable in a programming language. In most programming languages, an integer is typically represented using 4 bytes (32 bits) of memory. This means that when you declare an integer variable, 4 bytes of RAM will be allocated to store its value.

Similarly, let's say you have an array of 100 integers. Since each integer occupies 4 bytes, the array would require **100 \* 4 = 400 bytes** of RAM.

Different data structures have different memory requirements based on their design and the type of data they store. For instance:

1. Arrays: As mentioned earlier, arrays store elements of the same data type in contiguous memory locations. The memory required by an array is determined by multiplying the size of each element by the number of elements in the array.
    
2. Linked Lists: In a linked list, memory is dynamically allocated for each node. Each node contains both the data and a pointer/reference to the next node in the list. The memory required for a linked list depends on the number of nodes and the size of each node.
    
3. Trees: Trees consist of nodes connected in a hierarchical structure. Each node holds data and pointers to its child nodes. The memory needed for a tree depends on the number of nodes and the size of each node.
    

It's important to note that the memory usage of data structures is not limited to just the data they store. It also includes any additional metadata or overhead required by the programming language or the underlying implementation of the data structure.

Efficient memory management is a crucial consideration when designing and working with data structures. It helps ensure optimal utilization of RAM and avoids unnecessary memory wastage.

---

## 1\. Array

An array is a data structure in Kotlin that stores a fixed-size sequential collection of elements of the same type. In other words, an array is a container that holds a fixed number of elements of a specific type.

Declaring and initializing an array in Kotlin is easy. Here is an example of an array of integers:

```kotlin
val numbers: IntArray = intArrayOf(1, 2, 3, 4, 5)
```

In this example, we declare an array called `numbers` and initialize it with the values 1, 2, 3, 4, and 5. The `IntArray` type specifies that the array holds integers.

We can access individual elements of the array using their index, which starts at 0. For example, to access the first element of the `numbers` array, we can use the following code:

```kotlin
val firstNumber = numbers[0]
```

This assigns the value of the first element of the `numbers` array to the variable `firstNumber`. Similarly, we can access any other element of the array by specifying its index.

We can also modify individual elements of the array by assigning a new value to their index. For example, to change the value of the third element of the `numbers` array to 10, we can use the following code:

```kotlin
numbers[2] = 10
```

Arrays in Kotlin also provide several useful methods for working with their elements, such as `size`, which returns the number of elements in the array, and `forEach`, which applies a function to each element of the array.

```kotlin
arraySize = numbers.size // returns 5
numbers.forEach { println(it) } // prints each element of the array
```

Keep in mind that arrays in Kotlin have a fixed size, which means that once you declare an array, you cannot add or remove elements from it. If you need a collection that can grow or shrink dynamically, you may want to consider using a `List` instead.

---

### How an Array is stored in memory?

When an array is created in a programming language, the memory for the array is allocated in the computer's RAM (Random Access Memory) in a contiguous block of memory. The amount of memory required to store an array depends on the data type and the number of elements in the array.

For example, consider this array:

```kotlin
val numbers: IntArray = intArrayOf(1, 2, 3, 4, 5)
```

This creates an array of integers called `numbers` with a size of 5. The array can hold 5 integers, and each integer requires 4 bytes of memory on a typical **32-bit** system. Therefore, the total memory required to store the entire array is **5 \* 4 = 20 bytes**.

When the array is created, the memory for the array is allocated in the computer's RAM as a contiguous block of memory.

The starting address of this block of memory is stored in reference variable `numbers`.

Each element of the array is stored in a consecutive memory location, and the index of an element corresponds to its offset from the starting address of the array.

For example, let's say that the starting address of the array `arr` is 1000. Then, the memory locations for each element of the array would be as follows:

```kotlin
numbers[0]: 1000
numbers[1]: 1004
numbers[2]: 1008
numbers[3]: 1012
numbers[4]: 1016
```

As you can see, each element of the array is stored in a consecutive memory location, and the offset between two consecutive elements is equal to the size of the data type, which is 4 bytes in this case.

When an element of the array is accessed, the computer uses the starting address of the array and the index of the element to calculate the memory location of the element in the RAM. This process is very efficient and allows for fast and easy access to the elements of the array in O(1).

## 2\. List

list is a data structure that represents an ordered collection of elements, where each element has an associated index. It allows for efficient insertion, deletion, and retrieval of elements based on their positions in the list.

In Kotlin, the `List` the interface provides a read-only list, while the `MutableList` interface extends `List` to support the modification of elements.

Arrays and lists are similar in that they both store ordered collections of elements. However, there are some key differences:

* Size: Arrays have a fixed size defined at the time of creation, whereas lists can dynamically grow or shrink as elements are added or removed.
    
* Flexibility: Lists offer more flexibility in terms of resizing and modifying elements, while arrays are more static in nature.
    
* Memory Management: Arrays generally require less memory overhead, as they only store the elements themselves, whereas lists may require additional memory for managing their internal structures.
    

### How List works inside memory

When a dynamic list (also known as a dynamic array or resizable array) is stored in memory, it starts with an initial allocated capacity. As new items are added to the list and the capacity is exceeded, the list is resized by allocating a larger block of memory and copying the existing elements to the new block. Let's explore the process in more detail:

1. Memory Allocation: When the dynamic list is created, an initial block of memory is allocated to hold a certain number of elements. The size of this block depends on the implementation and may vary. The list also keeps track of the current number of elements and the allocated capacity.
    
2. Adding a New Item: When a new item is added to the dynamic list, the implementation checks if there is enough space in the allocated block to accommodate the new element.
    
    a. If there is available space: If the current number of elements does not exceed the allocated capacity, the new item is simply stored in the next available memory slot.
    
    b. If the capacity is exceeded: If the current number of elements exceeds the allocated capacity, the list needs to be resized. The implementation follows these steps:
    
    1. Allocate a new, larger block of memory: A new block of memory is allocated with an increased capacity. The new capacity can be determined based on various factors, such as doubling the current capacity or adding a fixed number of additional slots.
        
    2. Copy existing elements to the new block: The existing elements from the old block of memory are copied to the new block, ensuring their order is maintained.
        
    3. Update references and release old memory: The list updates the references to the new block and releases the old memory to free up resources.
        
    4. Add the new item: Finally, the new item is added to the next available memory slot in the resized list.
        
    
    This resizing process ensures that the dynamic list can accommodate additional elements beyond its initial capacity.
    

It's important to note that the resizing operation can be costly in terms of time and memory. The frequency of resizing can impact the performance of the dynamic list. To mitigate excessive resizing, some implementations may employ strategies such as resizing by a larger factor or using incremental resizing.

```kotlin
fun main() {
    // Creating a List
    val myList = listOf("apple", "banana", "orange", "kiwi")
    println("Original List: $myList")

    // Accessing Elements
    val firstElement = myList[0]
    println("First Element: $firstElement")

    // Modifying Elements (Creating a Mutable List)
    val mutableList = myList.toMutableList()
    mutableList[1] = "grape"
    println("Modified List: $mutableList")

    // Adding Elements
    mutableList.add("watermelon") // Adding an element to the end
    mutableList.add(2, "mango") // Inserting an element at index 2
    println("List after Adding Elements: $mutableList")

    // Removing Elements
    mutableList.remove("banana") // Removing an element by value
    mutableList.removeAt(0) // Removing an element at index 0
    println("List after Removing Elements: $mutableList")

    // Checking List Size and Empty
    val listSize = mutableList.size
    val isEmpty = mutableList.isEmpty()
    println("List Size: $listSize")
    println("Is List Empty? $isEmpty")

    // Iterating and Transforming Elements
    mutableList.forEach { element ->
        println("Processing element: $element")
    }

    val upperCaseList = mutableList.map { element ->
        element.toUpperCase()
    }
    println("List after Transforming to Upper Case: $upperCaseList")

    // Filtering Elements
    val filteredList = mutableList.filter { element ->
        element.length > 4
    }
    println("Filtered List: $filteredList")

    // Sorting Elements
    val sortedList = mutableList.sorted()
    println("Sorted List: $sortedList")
}
```

# 3\. HashMap

A HashMap is a data structure that provides fast access to values based on a unique key. It internally uses an array and a hashing function to map keys to specific indices in the array, allowing for efficient retrieval and storage of key-value pairs.Let's explore HashMaps with an example in Kotlin:

Consider a scenario where you want to store a collection of students and their corresponding grades using a HashMap.

```kotlin
fun main() {
    // Create a HashMap to store student grades
    val gradesMap = HashMap<String, Int>()

    // Add student grades to the HashMap
    gradesMap["John"] = 85
    gradesMap["Emily"] = 92
    gradesMap["Michael"] = 78

    // Accessing values from the HashMap
    val johnGrade = gradesMap["John"]
    println("John's Grade: $johnGrade")

    // Updating a value in the HashMap
    gradesMap["Emily"] = 95
    val updatedEmilyGrade = gradesMap["Emily"]
    println("Updated Emily's Grade: $updatedEmilyGrade")

    // Removing a value from the HashMap
    gradesMap.remove("Michael")
    val michaelGrade = gradesMap["Michael"]
    println("Michael's Grade: $michaelGrade")

    // Checking if a key exists in the HashMap
    val containsJohn = gradesMap.containsKey("John")
    println("Does the HashMap contain John? $containsJohn")
    
    // Iterating over the HashMap
    for ((student, grade) in gradesMap) {
        println("$student: $grade")
    }
}
```

Regarding how HashMap generates indices, it uses a hashing function to convert the keys into integer values called hash codes.

The hash codes are then mapped to specific indices in the underlying array using a process called hashing. This allows for efficient storage and retrieval of key-value pairs. The exact hashing algorithm used depends on the implementation of HashMap.

internally, a HashMap in Kotlin uses an array of linked lists (buckets) to store key-value pairs. The hashing function in Kotlin is responsible for converting the key into an integer value called the hash code.

This hash code is used to determine the index (bucket) in the array where the key-value pair will be stored. Let's dive into the internal workings of a HashMap:

1. Hashing Function:
    
    * The hashing function in Kotlin is implemented by the `hashCode()` method, which is defined in the `Any` class. All objects inherit this method, and it can be overridden for custom types.
        
    * The `hashCode()` method calculates a unique integer value (hash code) for each object based on its internal state. Objects that are considered equal should have the same hash code.
        
    * Kotlin provides default implementations of `hashCode()` for built-in types, such as `String`, `Int`, and `Boolean`.
        
2. Hashing and Index Calculation:
    
    * Once the hash code is obtained from the key, the HashMap applies a process called hashing to map the hash code to an index in the underlying array.
        
    * The index calculation is performed by applying a transformation to the hash code using bitwise operations and masking to ensure the index falls within the valid range of the array.
        
    * The specific algorithm for index calculation can vary based on the HashMap implementation.
        
3. Handling Collisions:
    
    * Since multiple keys can potentially have the same hash code or map to the same index, HashMap uses separate chaining to handle collisions.
        
    * Each index in the array can hold a linked list of key-value pairs. If multiple keys have the same index, they are stored in the corresponding linked list.
        
    * When retrieving a value, the HashMap uses the hash code and equality comparison to find the appropriate key-value pair in the linked list.
        
4. Resizing and Load Factor:
    
    * HashMap also implements resizing to maintain a balance between the number of key-value pairs and the capacity of the underlying array.
        
    * The load factor is a threshold that determines when to resize the HashMap. When the number of elements exceeds the load factor multiplied by the current capacity, the HashMap is resized by creating a new array with a larger capacity and rehashing all the key-value pairs into the new array.
        
    * Resizing allows for efficient storage and retrieval even as the number of key-value pairs increases.
        

It's important to note that the exact implementation details of hashing functions and collision resolution may vary depending on the HashMap implementation in different versions of Kotlin or different programming languages.

By leveraging the hashing function and handling collisions with linked lists, HashMap provides efficient storage and retrieval of key-value pairs based on their unique keys.

---

We will continue with [part 2](https://satyajitdas.tech/essential-data-structures-for-your-upcoming-android-interview-part-2), discussing the rest of the Data structures. Click [here](https://satyajitdas.tech/essential-data-structures-for-your-upcoming-android-interview-part-2) to read . Happy Coding !!