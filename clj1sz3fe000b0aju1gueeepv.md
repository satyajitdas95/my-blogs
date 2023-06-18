---
title: "Essential Data Structures for Your Upcoming Android Interview - Part 2"
seoTitle: "Crucial Android Interview Data Structures: Part 2"
seoDescription: "Master arrays, lists, hashmaps, sets, queues, stacks, trees, and graphs for efficient Android app development, optimizing code and performance"
datePublished: Sun Jun 18 2023 19:10:43 GMT+0000 (Coordinated Universal Time)
cuid: clj1sz3fe000b0aju1gueeepv
slug: essential-data-structures-for-your-upcoming-android-interview-part-2
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1687115017289/608439eb-4979-4c84-8475-deab7838edeb.avif
tags: android-app-development, data-structures, android, kotlin, dsa

---

If you haven't read Part One yet, click [here](https://satyajitdas.tech/essential-data-structures-for-your-upcoming-android-interview) to read it.

# 4\. Sets

In simple terms, a set is a data structure that represents a collection of unique elements. It's like a container that can hold different objects, but it only keeps track of each object once, even if it appears multiple times in the collection.

Think of it like a bag where you can put various items. However, in a set, you won't find any duplicates. If you try to add the same item to the set again, it won't change because the set already contains that item.

Sets are useful when you want to keep track of a group of distinct elements without worrying about their order or how many times they appear. You can perform operations on sets like adding elements, removing elements, or checking if a specific element is present in the set.

For example, imagine you have a set of fruits that includes an apple, a banana, and an orange. If you try to add another apple to the set, it won't make a difference because the set already has an apple. However, if you add a strawberry, it will be included because it's a new element. Similarly, if you remove the banana, it will no longer be part of the set.

```kotlin
fun main() {
    // Creating a set of fruits
    val fruitSet = mutableSetOf("apple", "banana", "orange")

    // Adding an element to the set
    fruitSet.add("strawberry")

    // Trying to add a duplicate element
    fruitSet.add("apple")

    // Removing an element from the set
    fruitSet.remove("banana")

    // Checking if an element is present in the set
    val containsOrange = fruitSet.contains("orange")
    val containsGrapes = fruitSet.contains("grapes")

    // Printing the set
    println(fruitSet)

    // Printing the results of the membership checks
    println("Contains orange: $containsOrange")
    println("Contains grapes: $containsGrapes")
}
```

Output -

```kotlin
[strawberry, apple, orange]
Contains orange: true
Contains grapes: false
```

Sets are often used in programming to solve problems involving uniqueness and membership checks efficiently.

# 5.Queue

a queue is a data structure that represents a collection of elements arranged in a specific order. It follows the principle of "first in, first out" (FIFO), which means that the element that enters the queue first will be the first one to be removed.

Think of a queue as a line of people waiting for something, such as waiting in line at a ticket counter or a bus stop. The person who arrives first is the first to be served or get on the bus, and as more people join the line, they stand behind the others. Similarly, in a queue data structure, elements are added at one end and removed from the other end.

You can perform two main operations on a queue:

1. Enqueue: This operation adds an element to the end of the queue. It represents joining the line or adding a new person to the back of the line.
    
2. Dequeue: This operation removes the element from the front of the queue. It represents serving the first person in line or the person who has been waiting the longest.
    

Queues are useful when you need to manage a sequence of elements where the order of insertion is important. They are commonly used in scenarios where elements arrive or need to be processed in a specific order, such as task scheduling, message processing, or breadth-first search algorithms.

```kotlin
import java.util.LinkedList

fun main() {
    // Create a queue
    val queue: Queue<String> = LinkedList()

    // Enqueue elements
    queue.offer("Element 1")
    queue.offer("Element 2")
    queue.offer("Element 3")

    // Dequeue elements
    val dequeuedElement = queue.poll()

    // Print the dequeued element
    println("Dequeued element: $dequeuedElement")

    // Peek at the front element without dequeuing
    val frontElement = queue.peek()

    // Print the front element
    println("Front element: $frontElement")

    // Print the entire queue
    println("Queue: $queue")
}
```

Output -

```kotlin
Dequeued element: Element 1
Front element: Element 2
Queue: [Element 2, Element 3]
```

In this example, we use the `LinkedList` class from the Java standard library to implement the queue. We create a queue called `queue` using the `Queue` interface.

We enqueue elements into the queue using the `offer` function, which adds elements to the rear of the queue.

Next, we dequeue an element from the front of the queue using the `poll` function, which also removes the element from the queue. The dequeued element is stored in the `dequeuedElement` variable.

We then use the `peek` function to access the front element of the queue without removing it. The front element is stored in the `frontElement` variable.

Finally, we print the dequeued element, the front element, and the entire queue.

Note that we're using the `Queue` interface, which provides basic queue operations like `offer`, `poll`, and `peek`. The `LinkedList` class is used as the concrete implementation of the queue, but you can also use other implementations such as `ArrayDeque`.

# 6.Stack

A Stack is a data structure that represents a collection of elements in a specific order. It follows the principle of "last in, first out" (LIFO), which means that the element that enters the stack last will be the first one to be removed.

Think of a stack like a stack of plates. When you add a new plate, you place it on top of the stack. Similarly, when you remove a plate, you take the one from the top. The last plate you put on the stack is the first one you can access or remove.

You can perform two main operations on a stack:

1. Push: This operation adds an element to the top of the stack. It represents placing a new plate on top of the stack.
    
2. Pop: This operation removes the element from the top of the stack. It represents taking the plate from the top of the stack.
    

Stacks are useful when you need to manage elements in a last-in, first-out manner. They are commonly used in scenarios where you want to keep track of the order of operations or process elements in reverse order, such as function call stacks, undo/redo functionality, or parsing expressions.

This is how to stack internal implementation looks like

```kotlin
class Stack<T> {
    private val stackList = mutableListOf<T>()

    fun push(element: T) {
        stackList.add(element)
    }

    fun pop(): T? {
        if (stackList.isEmpty()) {
            return null
        }
        val lastIndex = stackList.size - 1
        return stackList.removeAt(lastIndex)
    }

    fun peek(): T? {
        if (stackList.isEmpty()) {
            return null
        }
        val lastIndex = stackList.size - 1
        return stackList[lastIndex]
    }

    fun isEmpty(): Boolean {
        return stackList.isEmpty()
    }

    fun size(): Int {
        return stackList.size
    }
}

fun main() {
    val stack = Stack<Int>()

    stack.push(1)
    stack.push(2)
    stack.push(3)

    println("Stack size: ${stack.size()}")
    println("Top element: ${stack.peek()}")

    val poppedElement = stack.pop()
    println("Popped element: $poppedElement")

    println("Is the stack empty? ${stack.isEmpty()}")
}
```

Output -

```kotlin

Stack size: 3
Top element: 3
Popped element: 3
Is the stack empty? false
```

In Android development, the stack data structure is commonly used in various scenarios, including:

1. Activity Stack: Android uses a stack to manage the activity lifecycle. When a new activity is launched, it is placed on top of the activity stack. When the user navigates back, the top activity is popped from the stack and the previous activity is resumed. This allows for a hierarchical flow of activities, with the back button behaviour following a stack-like structure.
    
2. Fragment Back Stack: Fragments in Android can also be managed using a stack-like structure. Fragments are added to a back stack, and when the user navigates back, the top fragment is popped and the previous fragment is shown. This enables navigation within a single activity using the Fragment Manager.
    
3. Undo/Redo Functionality: Android apps often provide undo and redo functionality for user actions. A stack data structure can be used to store the history of actions, allowing users to revert or redo their actions by popping or pushing elements onto the stack.
    
4. Navigation History: Navigation within Android apps, especially those using navigation components like Navigation Architecture Component, often relies on a stack-like structure. As users navigate through different screens or destinations, the app maintains a navigation stack, allowing users to navigate back through the history of visited screens.
    
5. Input Events: In certain cases, the stack data structure can be utilized to manage input events or tasks that need to be processed in a specific order. For example, if an app receives a stream of user inputs, the inputs can be pushed onto a stack and processed in reverse order, ensuring that the most recent input is handled first.
    

These are just a few examples of how the stack data structure is used in Android development. Stacks are particularly useful in scenarios involving hierarchical or sequential operations where the last item processed or accessed needs to be prioritized.

# 7.Tree

Certainly! Think of a tree data structure as a visual representation of a hierarchical relationship between elements. Just like a tree in nature, a tree data structure has a root at the top, branches that extend downwards and leaves at the bottom.

* Root: The root is the starting point of the tree. It is the topmost node and has no parent. Think of it as the base of the tree.
    
* Node : Each element in the tree is called a node. A node can have some associated data and can be connected to other nodes.
    
* Parent and Child: Nodes in a tree have parent-child relationships. A parent node is connected to its child nodes, and child nodes are connected to their parent. A node can have multiple child nodes but only one parent.
    
* Leaf: A leaf is a node that does not have any children. It is at the bottom of the tree.
    
* Branch: A branch is a connection between a parent node and its child node. It represents the path from one node to another.
    
* Depth: The depth of a node is the number of edges from the root to that node. The depth of the root node is 0, and the depth of other nodes increases as you move down the tree.
    
* Height: The height of a tree is the length of the longest path from the root to any leaf node. It represents the overall height of the tree.
    
* Subtree: A subtree is a smaller tree within the main tree, consisting of a node and all its descendants (children, grandchildren, and so on).
    

Tree data structures are useful for organizing hierarchical data, such as file systems, organization charts

Here's an example of implementing a basic tree data structure in Kotlin:

```kotlin
class TreeNode<T>(val data: T) {
    val children: MutableList<TreeNode<T>> = mutableListOf()

    fun addChild(child: TreeNode<T>) {
        children.add(child)
    }
}

fun main() {
    // Create a tree
    val root = TreeNode("A")

    val nodeB = TreeNode("B")
    val nodeC = TreeNode("C")
    val nodeD = TreeNode("D")

    val nodeE = TreeNode("E")
    val nodeF = TreeNode("F")

    root.addChild(nodeB)
    root.addChild(nodeC)
    root.addChild(nodeD)

    nodeB.addChild(nodeE)
    nodeB.addChild(nodeF)

    // Traverse the tree
    traverseTree(root)
}

fun traverseTree(node: TreeNode<String>) {
    println(node.data)

    for (child in node.children) {
        traverseTree(child)
    }
}
```

Output:

```kotlin
A
B
E
F
C
D
```

In this example, we define a `TreeNode` class that represents a node in the tree. Each node contains some data and a list of child nodes.

We create a tree by creating instances of `TreeNode` and connecting them using the `addChild` function. The root node is "A", and we add nodes "B", "C", and "D" as its children. Node "B" has children "E" and "F".

To traverse the tree, we define a `traverseTree` function that takes a `TreeNode` as a parameter. It prints the data of the current node and then recursively calls itself on each child of the node, traversing the tree in a depth-first manner.

In the `main` function, we create the tree and initiate the traversal by calling `traverseTree` with the root node.

---

### The Tree data structure in the **Jetpack compose**\-

Jetpack Compose uses a tree data structure internally to represent the composition of its UI. This allows Compose to efficiently manage the layout and rendering of its UI, as well as to support features such as hot reload and state management.

Here is an example of how Jetpack Compose uses a tree data structure to represent a simple UI:

```kotlin
@Composable
fun RootUI() {
    Column {
        Button(onClick = { /*TODO*/ }) {
            Text(text = "Button 1")
        }

        Button(onClick = { /*TODO*/ }) {
            Text(text = "Button 2")
        }
    }
}
```

When Compose renders this UI, it will first create a visual tree based on the tree data structure. This visual tree will then be used to render the UI on the screen.

```kotlin
RootUINode
  |
  ColumnNode
    |
    ButtonNode("Button 1")
    |
    ButtonNode("Button 2")
```

Jetpack Compose's use of a tree data structure makes it a very efficient UI framework. This is because Compose can easily update the visual tree when the state of its UI changes. This is what allows Compose to support features such as hot reloading, which allows you to see changes to your UI without having to rebuild your app.

Here is an example of how Compose uses a tree data structure to support hot reload:

```kotlin
@Composable
fun MyApp() {
  // Create a root node.
  val root = ComposeNode()

  // Add a Text node to the root node.
  root.add(Text("Hello, world!"))

  // Set a state variable.
  val text = mutableStateOf("Hello, world!")

  // Update the Text node when the state variable changes.
  LaunchedEffect(key1 = text) {
    while (true) {
      // Update the Text node with the current value of the state variable.
      root.update(0, Text(text.value))

      // Wait for a change to the state variable.
      text.awaitChange()
    }
  }

  // Return the root node.
  return root
}
```

When the state variable `text` changes, Compose will update the Text node in the visual tree. This will cause the UI to be updated without having to rebuild the app.

Jetpack Compose's use of a tree data structure is a powerful feature that makes it a very efficient and flexible UI framework.

# 8\. Graph

Imagine you have a group of friends and you want to represent their relationships using a graph. Each person is a node, and the connections between them are represented by edges.

In a graph, you have nodes (also called vertices) and edges. Nodes represent individual entities, like people, while edges represent the relationships or connections between them.

For example, let's say we have three friends named Alice, Bob, and Carol. We can represent them as nodes in the graph. If Alice is friends with Bob and Carol, and Bob is friends with Carol, we can connect these nodes with edges to represent their relationships.

Here's a simple visual representation:

```markdown
        Alice
        /   \
      Bob   Carol
```

In this graph, we have three nodes (Alice, Bob, and Carol) connected by two edges. Alice is connected to both Bob and Carol, while Bob is connected to Carol.

In a graph:

* Nodes (vertices): These are entities or objects represented as points in the graph. Each node can contain additional data or attributes.
    
* Edges: These are the connections between nodes. Edges can be directed (one-way) or undirected (two-way). They represent the relationships or connections between nodes.
    
* Weight: Edges can also have weights or costs associated with them. These weights can represent various properties, such as distance, cost, or any other relevant metric.
    

Graphs can be classified into two main types based on the presence or absence of directed edges:

1. Directed Graph (Digraph): In a directed graph, each edge has a specific direction. The edges indicate a one-way relationship between nodes.
    
2. Undirected Graph: In an undirected graph, edges have no direction. The relationships between nodes are bidirectional.
    

Graphs can have various structures, including:

* Cyclic: A graph with at least one cycle (a path that starts and ends at the same node).
    
* Acyclic: A graph that does not contain any cycles.
    
* Connected: A graph in which there is a path between any two nodes.
    
* Disconnected: A graph in which there are one or more isolated components, with no paths connecting them.
    

Graphs can also have more complex structures. For example, a social network can have hundreds or thousands of nodes representing users, with edges representing friendships between them.

---

### Use of Graph In Dagger/Hilt

Both Dagger and Hilt use a graph data structure to represent the dependencies between classes in your app. This graph is used to determine which classes need to be created and how they should be injected with dependencies.

Dagger uses a compile-time graph, which means that the graph is generated at compile-time. This makes Dagger faster than Hilt, but it also makes it more difficult to change the dependencies in your app.

Hilt uses a runtime graph, which means that the graph is generated at runtime. This makes Hilt slower than Dagger, but it also makes it easier to change the dependencies in your app.

Here is an example of a graph that Hilt might generate for an Android app:

**Code snippet**

```kotlin
class MainActivity {
    @Inject
    lateinit var viewModel: ViewModel

    fun onCreate() {
        // Hilt will inject the viewModel dependency into this class.
    }
}

class ViewModel {
    @Inject
    lateinit var userRepo: UserRepo

    @Inject
    lateinit var newsRepo: NewsRepo

    fun doSomething() {
        // Hilt will inject the repository dependency into this class.
    }
}

class UserRepo {

}

class NewsRepo {

}
```

In this example, the `MainActivity` class depends on the `ViewModel` class, and the `ViewModel` class depends on the `Repository` class. Hilt will generate a graph that represents these dependencies.

When Hilt needs to create an instance of `MainActivity`, it will traverse the graph and find all of the dependencies that `MainActivity` needs. Hilt will then create instances of those dependencies and inject them into `MainActivity`.

Hilt uses this process to generate instances of all of the classes in your app and to inject them with their dependencies. This allows you to write code that is independent of specific implementations of dependencies.

Example of A Dagger/Hilt Graph -

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687099692567/93937afa-ee13-4227-a097-66346e1de1de.png align="center")

---

# Conclusion

In conclusion, understanding data structures is crucial for successful Android app development. In this blog, we have explored various fundamental data structures such as arrays, lists, hashmaps, sets, queues, stacks, trees, and graphs. These structures serve as the building blocks for organizing and manipulating data efficiently in your app.

Sure, here is a good conclusion for a blog where you have explained about data structures like arrays, lists, hashmaps, sets, queues, stacks, trees, and graphs for Android app development:

In conclusion, data structures are an essential part of Android app development. They provide a way to store and organize data in a way that is efficient and easy to access. There are many different data structures available, and the best one to use will depend on the specific needs of your app.

Here is a quick summary of the data structures that we have discussed:

* Arrays: Arrays are a simple data structure that stores data in a contiguous block of memory. They are efficient for storing data that is accessed in sequential order.
    
* Lists: Lists are a more flexible data structure than arrays. They can store data in any order, and they can be easily modified.
    
* HashMaps: HashMaps are a data structure that stores data in a key-value pair. They are efficient for storing data that is accessed by its key.
    
* Sets: Sets are a data structure that stores data in a unique collection. They are efficient for storing data that does not need to be accessed in any particular order.
    
* Queues: Queues are a data structure that stores data in a first-in, first-out (FIFO) order. They are efficient for storing data that needs to be processed in a specific order.
    
* Stacks: Stacks are a data structure that stores data in a last-in, first-out (LIFO) order. They are efficient for storing data that needs to be processed in reverse order.
    
* Trees: Trees are a data structure that stores data in a hierarchical order. They are efficient for storing data that needs to be accessed by its relationship to other data.
    
* Graphs: Graphs are a data structure that stores data in a network of nodes and edges. They are efficient for storing data that needs to be processed in a complex way.
    

Having a solid understanding of these data structures enables you to design and implement efficient algorithms, optimize memory usage, and enhance the overall performance of your Android app.

It allows you to choose the most suitable data structure based on the requirements of your application, ensuring better user experiences and smoother functionality.

Remember, selecting the appropriate data structure requires careful consideration of factors such as data access patterns, search requirements, insertion and deletion operations, and memory usage. Additionally, continuously improving your knowledge of data structures and algorithms will empower you to tackle more complex problems and make your Android app development journey even more successful.

So, take the time to master these foundational data structures, experiment with them, and explore their capabilities within the context of Android app development. By doing so, you'll be equipped with the tools to create efficient, scalable, and robust applications that deliver exceptional user experiences.

I hope this blog has helped you to understand the basics of data structures and how they can be used in Android app development. If you have any questions, please feel free to leave a comment below. Happy coding!