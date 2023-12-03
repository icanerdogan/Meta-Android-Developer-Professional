## Advanced classes, nullability and collections

### Data Classes

As demonstrated in the first module, basic values like String or Int can be compared or printed.  However, objects created from custom classes behave somewhat differently. Let’s examine what happens when you compare or print these objects, and then discuss how this behavior can be altered using a special class modifier called **data**.

```kotlin
fun main() {
println("A" == "A") // true
println("A" == "B") // false
}
```

Let's say that you have a very simple class. You can compare it to itself, but this comparison will only return **true**, if exactly the same instance is on both sides of the comparison. This means that by default, all objects created with custom classes are considered unique, they are not equal to any other object.

```kotlin
class Dog(
val name: String
)

fun main() {
val pluto1 = Dog("Pluto")
val pluto2 = Dog("Pluto")

println(pluto1 == pluto2) // false
println(pluto1 == pluto1) // true
}
```

Printing or transforming an object into a string is also not very useful. The result should be this class name, @ sign, and some numeric digits. The number is not really useful, it only helps us know if two objects are the same or not.

```kotlin
println(pluto1) // Dog@404b9385
println("Dog: $pluto1") // Dog: Dog@404b9385
```

So, what can you do to get more meaningful data from printing a string? This behavior can be altered if you use **data** modifier before a class. You use it before classes representing a bundle of data. Such a class is equal to a different instance of the same class if its constructor properties have the same value.

```kotlin
data class Dog(
val name: String
)

fun main() {
val pluto1 = Dog("Pluto")
val pluto2 = Dog("Pluto")
val rex = Dog("Rex")

println(pluto1 == pluto2) // true
println(pluto1 == pluto1) // true
println(pluto1 == rex) // false
}
```

When you transform a data class into a string, you not only have this class name, but also values for each constructor property.

```kotlin
println(pluto1) // Dog(name=Pluto)
println("Dog: $pluto1") // Dog: Dog(name=Pluto)
```

That is not all. Data classes can be destructured, which means reading values from this class and assigning them to variables.

```kotlin
data class Dog(
val name: String,
val age: Int
)

val dog = Dog("Pluto", 7)
val (name, age) = dog
println(name) // Pluto
println(age) // 7
```

Beware that destructuring in Kotlin is based on position, not name, so value names need to be placed at correct positions. For instance, if you place **age** at the position of name, and **name** at the position of **age**, then you will have age in a variable called **name**, and name in the variable called **age**.

```kotlin
data class Dog(
val name: String,
val age: Int
)

fun main() {
val dog = Dog("Pluto", 7)
val (age, name) = dog
println(age) // Pluto
println(name) // 7
}
```

To prevent this, always check if your variables are assigned to the correct positions of constructor parameters.

Finally, data classes have a **copy** method, that creates a copy of an object. It also allows you to specify what modifications you would like to introduce into an object.

```kotlin
data class Dog(
val name: String,
val age: Int
)

fun main() {
println(dog.copy()) // Dog(name=Pluto, age=7)
println(dog.copy(age = 8)) // Dog(name=Pluto, age=8)
println(dog.copy(name = "Neptune")) // Dog(name=Neptune, age=7)
}
```

### **Pair and Triple**

In some cases, you need to represent a pair of values. For that, a class you can use is the **Pair** class. This is a data class with two constructor properties, you do not need to define it, as it is distributed with Kotlin.

In the below example, a pair with values of type **Double** and **Char** is created. You can read those values using **first** and **second** properties. You can also destructure it into variables.

```kotlin
fun main() {
val pair = Pair(1.0, 'A')
println(pair.first) // 1.0
println(pair.second) // A
val (number, letter) = pair
    // the type of number is Double
    // the type of letter is Char
println(number) // 1.0
println(letter) // A
}
```

There is also another way to create a pair: by placing the **to** function between two values. The result is a pair of those two values.

```kotlin
fun main() {
val pair = 1.0 to 'A'
println(pair.first) // 1.0
println(pair.second) // A
val (number, letter) = pair
    // the type of number is Double
    // the type of letter is Char
println(number) // 1.0
println(letter) // A
}
```

Another such class is called **Triple**, and it is used to keep three values on properties **first**, **second** and **third**.

```kotlin
fun main() {
val pair = Triple(1F, "ABC", true)
println(pair.first) // 1.0
println(pair.second) // ABC
println(pair.third) // true
val (number, letters, boolean) = pair
    // the type of number is Double
    // the type of letters is Char
    // the type of boolean is Boolean
println(number) // 1.0
println(letters) // ABC
println(boolean) // true
}
```

### Enum Classes

### Examples of **enum** classes

Use **enum** classes whenever you need to define a specific set of values.

Let's say that you need to express a day of the week. A good choice is to define an **enum** class with the seven possible options:

```kotlin
enum class WeekDay {
    SUNDAY,
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY
}
```

In a game, you could specify a difficulty level using an **enum**:

```kotlin
enum class Difficulty {
    EASY,
    MEDIUM,
    HIGH
}
```

You could also use an **enum** class to specify possible pizza sizes:

```kotlin
enum class PizzaSize {
    SMALL,
    MEDIUM,
    LARGE,
    EXTRALARGE
}
```

### Defining values in **enum** classes

**Enum** class can also have a constructor. It looks just like a constructor in regular classes, but when it is defined, each value needs to call it. This mechanism is used to assign values to each **enum** value. For instance, in the pizza sizes example, it could be a size in centimeters.

```kotlin
enum class PizzaSize(
val sizeInCm: Int
) {
SMALL(15),
MEDIUM(20),
LARGE(25),
EXTRALARGE(30)
}

fun printSize(pizzaSize: PizzaSize) {
    println("$pizzaSize is ${pizzaSize.sizeInCm} cm")
} 

fun main() {
    printSize(PizzaSize.MEDIUM) // MEDIUM is 20 cm
    printSize(PizzaSize.EXTRALARGE) // EXTRALARGE is 30 cm
}
```

### Exceptions

In this reading, you will review the process of throwing and catching exceptions, learn about exception reports and learn to use **finally block**.

### Defining and throwing exceptions

Any class that extends **Throwable** can be used as an exception. That means it can be thrown using a **throw** block. Such an exception immediately ends functions unless it is caught with a **try-catch** block.

```kotlin
class MyError: Throwable("Some message")

fun someFunction() {
    throw MyError()
println("Will not be printed")
}

fun main() {
    try {
someFunction()
println("Will not be printed")
    } catch (e: Throwable) {
println("Caught $e") // Caught MyError: Some message
    }
}
```

### Exception report and stack trace

When an exception is not caught, it ends the program. As a result, there is printed information about this exception.

```kotlin
class MyError: Throwable("Some message")

fun someFunction() {
    throw MyError()
println("Will not be printed")
}

fun main() {
someFunction()
println("Will not be printed")
}
```

**Result:**

```kotlin
Exception in thread "main" MyError: Some message
at TestKt.someFunction(Test2.kt:4)
at TestKt.main(Test2.kt:9)
at TestKt.main(Test2.kt)
```

This information about exceptions, known as an exception report, is really useful. First, it tells you the type of exception and its message. Message is a parameter from **Throwable**, that is often specified when you throw an exception. There is also a structure called **stack trace**, that tells you where this exception was thrown. An exception is thrown in a function, that was invoked in another function, that was invoked in another function and so on. To fully represent that, you should not only show where **throw** was used, but also where this function was called, and so forth. As a result, you have a whole stack of functions, and for each of them, stack trace prints its name, class, and the line where exception occurred. Reading stack trace is really useful, when you are debugging your program, that is to say, finding and fixing mistakes

### **Finally** block

Inside **try**, you can also use a block called **finally**. It is used to specify a block of code that should always be invoked, even if an exception occurs. Take a look at the code below. Inside **someFunction** an exception is thrown. It ends the function, and it ends the body of **try**. Since you do not have **catch block,** this exception will not be caught, and it will end the 'main' function. However, there is the **finally block** that is invoked even if an exception occurs.

```kotlin
fun someFunction() {
    throw Throwable("Some error")
println("Will not be printed")
}

fun main() {
    try {
someFunction()
println("Will not be printed")
    } finally {
println("Finally block was called") // Finally block was called
    }
println("Will not be printed")
}
```

The **finally** block is also invoked when the **try** block finishes without an exception.

```kotlin
fun someFunction() {
println("Will be printed") // Will be printed
}

fun main() {
    try {
someFunction()
println("Will be printed") // Will be printed
    } finally {
println("Finally block was called") // Finally block was called
    }
println("Will be printed") // Will be printed
}
```

**finally block** is used to do operations that should always be done, no matter if an exception occurred or not. It typically involves closing connections or cleaning-up resources.

### Important exceptions

There are a few kinds of exceptions defined in Kotlin that are used in certain situations. The most important ones are:

- **IllegalArgumentException** used when an argument has an incorrect value. For example, when you expect your argument value to be bigger than 0, and it is not.
- **IllegalStateException** used when the state of our system is incorrect. That means the values of properties have values that are not accepted by our function call.

```kotlin
fun findClusters(number: Int) {
    if (number < 1) throw IllegalArgumentException("The number of clusters cannot be smaller than 1, it is $number")
    // ...
}

var userName = ""

fun printUserName() {
    if (userName == "") throw IllegalStateException("User name must not be empty")
    // ...
}
```

### Sealed Classes

### Sealed classes and interfaces

As explained in a previous module, classes connected in parent-child relationships form hierarchies. For instance, when you have an abstract class **Animal**, with subclasses **Dog** and **Cat**, they are in a relationship one to another, and they form a hierarchy of objects.

```kotlin
abstract class Animal
class Dog : Animal()
class Cat : Animal()
```

Such a hierarchy is called **open**, because one can always define another class that inherits from **Animal**. That makes a lot of sense, there is no limit to the number of animal types. However, this is not true for all the hierarchies. Consider that you try to make a network operation. The result is either a success or a failure. You do not want to allow anyone to define any other subclasses. That is a case for using a **sealed** modifier instead of **abstract**.

```kotlin
sealed class Result
class Success(val data: String) : Result()
class Failure(val exception: Throwable) : Result()
```

A **sealed** modifier used in front of a class behaves just like **abstract**, but it also introduces some limitations.

Officially subclasses of a sealed class need to be defined in the same package. What is more important is that a **sealed** modifier is information to the developer who reads the code - it informs them that this class has a limited number of subclasses known in advance during compilation.

### Sealed classes and **when** expressions

There is one important consequence of using sealed classes. You might remember that using **when** as an expression, you need to specify an **else** block so that there is always something returned.

```kotlin
fun constructLabel(role: String, name: String): String {
    return when (role) {
        "ceo" -> "The boss"
        "manager" -> "Manager $name"
        "worker" -> name
        else -> "Unknown role"
    }
}

fun main() {
val label = constructLabel("manager", "Leonard")
println(label) // Manager Leonard
}
```

There are exceptions to this rule. As demonstrated previously, you do not need to specify **else** if you when expression with an enum class, and you cover all the possible values.

```kotlin
enum class Role {
    CEO,
    MANAGER,
    WORKER
}

fun constructLabel(role: Role, name: String): String {
    return when (role) {
        CEO -> "The boss"
        MANAGER -> "Manager $name"
        WORKER -> name
    }
}

fun main() {
val label = constructLabel(Role.MANAGER, "Leonard")
println(label) // Manager Leonard
}
```

Another such exception is when you use **when** with a sealed class value, and you cover all the possible subtypes. Take a look at the code below. Since it covers all the possible subtypes of **Role** in a **when** expression, you do not need to specify an **else** block. It is possible thanks to the **sealed** modifier.

```kotlin
sealed class Role
class CeoRole(): Role()
class ManagerRole(val name: String): Role()
class WorkerRole(val name: String): Role()

fun constructLabel(role: Role): String {
    return when (role) {
        is CeoRole -> "The boss"
        is ManagerRole -> "Manager ${role.name}"
        is WorkerRole -> role.name
    }
}

fun main() {
val label = constructLabel(ManagerRole("Leonard"))
println(label) // Manager Leonard
}
```

### Annotation Classes

The last special kind of class is called **annotation**. Annotations are classes used to describe your code. For example, let's say that your function throws an exception. To inform other coders that may use our class about such a possibility, you can add annotation **Throws** with an exception class.

```kotlin
@Throws(ArithmeticException::class)
fun divide(a: Int, b: Int): Int {
    return a / b
}

@Throws(IllegalArgumentException::class)
fun findClusters(number: Int) {
    if (number < 1) throw IllegalArgumentException("The number of clusters cannot be smaller than 1, it is $number")
    // ...
}
```

It is important to understand that an annotation by itself does absolutely nothing. However, annotations are often defined by libraries that analyze your code and change its behavior based on an annotation. Some annotations are also used by Kotlin itself. For instance, let's say that you defined a class with certain methods, but over time you decide to introduce an alternative method for doing the same operation. The problem is that the old method is still used by other parts of your program. What should you do? The answer is using **Deprecated** annotation before the old method. Such annotation is interpreted by the Kotlin compiler and IntelliJ, and results in old functions usages being presented as crossed out and a warning with the message specified in the annotation. This is a good mechanism to inform users of your class that the old method should not be used anymore, and what they should replace it with. When enough time has passed (typically a period of least a year is acceptable), then you might assume that all the users adjusted their code to stop using the deprecated method, and you can finally remove it.

We rarely define custom annotations in regular projects, but to demonstrate that they are nothing special, let's explore the following example of an annotation class definition and its usage.

```kotlin
annotation class MyAnnotation(val someDescription: String)

@MyAnnotation("Class annotation")
class A(
    @MyAnnotation("Constructor property annotation")
val a: Int
) {
    @MyAnnotation("Method annotation")
    fun b() {}
}
```

### Nullability & Nullable

Part of Kotlin’s language design is to avoid errors due to null values. The following code demonstrates this design choice.

```kotlin
var message: String = "Hello World"
message = null // compilation error
```

It is not possible to assign a null value to the message variable, and the compiler will display an error.

### Null pointer exception (NPE)

When accessing a property or using a function of a non-nullable type, it is always guaranteed not to cause (or throw) a type of error called a null pointer exception (NPE).

```kotlin
var length = message.length // This always works
```

### Defining a **null** value

Sometimes you will need a way to represent **“no value”** using null.

To do this, use the question mark symbol when defining the variable type. The following is an update to the previous example to be a nullable type by adding the question mark symbol after the string type.

```kotlin
var message: String? = "Hello World"
message = null // this is ok
```

The risk of using nullable types is that if you try to access a property or function on a variable that is currently assigned a null value, it will cause an NPE.

For example, if you try to access the length property of the message variable while the message variable is null, the exception will be thrown.

```kotlin
var message: String? = "Hello World"
message = null //Assign null to the variable
var length = message.length // Will cause a Null Pointer Exception
```

To avoid these errors, you will need to check for a null value before accessing the property. Here’s the update for the previous example to check for null.

```kotlin
var message: String? = "Hello World"

message = null // Assign null to the variable

if (message != null) {

    var length =
        message.length // Will not cause an error because you have checked that the value is not null

    print(length)
} else {

    print(null)
}
```

### **Safe call**

Another way to avoid the error is to use a **safe call**.

The safe call is when **?.**  is used instead of  **.** between an object and its function or property. A safe call calls the right side if the left side is not null. Otherwise, it does nothing and returns null.

Let’s update the previous example to use a safe call.

```kotlin
var message: String? = "Hello World"
print(message?.length) //Will print 11
message = null //Assign null to the variable
print(message?.length) //Will print null
```

Similarly, if you call a function using the safe call, it will do nothing. Let’s update the example to call the uppercase String function.

```kotlin
var message: String? = "Hello World"
print(message?.uppercase()) //Will print HELLO WORLD
message = null //Assign null to the variable
print(message?.uppercase()) //Will print null
```

### Smart Casting

ou might recall that smart-casting is a Kotlin capability that can change the type of variable for a scope, but only if Kotlin knows that the variable is of that type in the scope.

For example, if you have a parameter **a** of type **Any**, and you add the condition **if(a is String)**, then in the scope of such check, the variable **a** changes its type to **String**, and then you might ask for its **length**.

```kotlin
fun consume(a: Any) {
    if (a is String) {
println(a.length) // the type of a is String
    }
    if (a is Int) {
println(a * 10) // the type of a is Int
    }
}

fun main() {
    consume("ABC") // 3
consume(10) // 100
}
```

Smart-casting can also be used to deal with nullability. When you have a nullable type and a check that it is not null, Kotlin knows that it is not null when the variable is subsequently used.

```kotlin
fun consume(a: String?) {
    if (a != null) {
println(a.length) // the type of a is String
    } else {
println("Cannot handle null")
    }
}

fun main() {
    consume("ABC") // 3
    consume(null) // Cannot handle null
}
```

Smart-casting is quite powerful and works in a variety of configurations.

```kotlin
fun consumeA(a: String?) {
    if (a == null || a.length == 0) return // after || a is smart-casted to String
println(a.length) // the type of a is String
}

fun main() {
    consume("ABC") // 3
    consume(null)
consume("")
}
```

However, smart-casting has some limitations. You cannot smart-cast read-write properties. This is due to safety concerns. Kotlin does not have a guarantee that the value of such a property hasn't been changed between check and usage by some other part of the program.

```kotlin
var a: String? = null

fun main() {
    a = "Sam"
    if (a != null) {
println(a.length) // COMPILATION ERROR, smart-casting not allowed
    }
}
```

### Collections

### What is the collections?

In this tutorial, the importance of collections in programming, specifically in Kotlin, is emphasized. The need for collections arises in scenarios where the number of elements is dynamic and may change over time, such as in an online shop with varying products, sellers, buyers, and payment/delivery methods.

Collections are crucial in programming, and various types are discussed in the course. The focus is on lists, which are a common collection type in Kotlin. To create a list, the `listOf` function is used, specifying values as arguments. An example list with three elements—tomatoes, spaghetti, and chicken—is demonstrated.

Lists can be transformed into strings, either by printing the list directly or by using a string template. Iterating over list elements is achieved through a `for` loop, where each element is processed in the loop body. The `size` property helps determine the number of elements in a list.

Notably, lists in Kotlin are read-only, meaning their internal structure cannot be changed. However, a new list can be created with modifications using the plus or minus sign. Removing an element creates a new list without that element, while adding an element results in a new list with the added element.

In summary, the tutorial provides a foundational understanding of Kotlin collection types, with a specific focus on lists and their creation, transformation, iteration, size determination, and modification functionalities.

### List, Set & Map

In this tutorial, Kotlin's various collection types are explored, namely lists, sets, and maps, each serving specific purposes in different scenarios. Lists represent ordered collections that allow duplicate elements, useful for scenarios like product listings in an online shop or delivery method options.

Sets, on the other hand, represent unordered collections without duplicates. They are suitable when order preservation is not important, such as storing a list of unique dog names.

Maps differ from lists and sets by holding key-value pairs. Keys are unique, mapping to exactly one value. Maps are valuable for storing logical connections between objects, like using an employee's unique ID as a key and their position as the corresponding value.

The tutorial also touches on the concept of read-only and mutable collections. By default, Kotlin collections are read-only, meaning their structure cannot change. However, a copy with additional values can be created. The distinction between immutable and mutable is demonstrated using both lists and strings, highlighting that while the collection structure remains constant, the values within can be modified for mutable collections.

Additionally, the hierarchy of interfaces representing collections is discussed. Most collections implement iterable and collection interfaces, with mutable collection interfaces being subtypes of their readable counterparts. This means that operations available for readable collections are also applicable to mutable ones.

The tutorial concludes by emphasizing the variety of classes implementing these interfaces, such as ArrayList and LinkedList for lists, each with distinct performance characteristics. Learners are encouraged to understand when to use specific collection types and grasp the distinction between read-only and mutable variants.

Overall, the tutorial equips learners with a comprehensive understanding of Kotlin collections, empowering them to make informed decisions when handling diverse data structures in their projects.

### Create a List

In this reading, you will learn how to create a list using the **listOf** function to:

- add elements to lists
- get elements at certain positions
- check if a list contains an element
- iterate over a list
- make and use a mutable list

### List

**List** is the most basic type of collection. It represents an ordered list of elements. The same elements can be repeated multiple times. You might use a list to represent products in a shopping cart or delivery method options. The order of elements is preserved, so if you define a list of delivery methods in some configuration, those elements should be displayed in the same order on the payment window.

**Creating a list**

To create a list, the **listOf** function is used. The next values are then specified using arguments.

```kotlin
fun main() {
    val list = listOf("A", "B", "C")
    println(list) // [A, B, C]
}
```

The result type is **List<T>**, where **"T"** is the type of elements in this list. Since the code above consists of a list with string values, the type is **List<String>**.

```kotlin
fun main() {
    val list: List<String> = listOf("A", "B", "C")
    println(list) // [A, B, C]
    val ints: List<Int> = listOf(1, 2, 3)
    println(ints) // [1, 2, 3]
}
```

**Adding elements to lists**

The easiest way to add elements to lists is using the plus sign. You can add a single element to a list, or you can add two lists together.

```kotlin
fun main() {
    val list = listOf("A", "B")
    println(list + "C") // [A, B, C]
    println(list + listOf("C", "D")) // [A, B, C, D]
    println(listOf("Z") + list) // [Z, A, B]
}
```

**Getting the size of a list**

You can always check the number of elements in a list using the **size** property.

```kotlin
fun main() {
    val list = listOf("A", "B", "C")
    println(list.size) // 3
}
```

To check if a list is empty, you can compare its size to **0**, or you can use the **isEmpty** method.

```kotlin
fun main() {
    val list = listOf("A", "B", "C")
    println(list.size == 0) // False
    println(list.isEmpty()) // False

    val empty: Set<Int> = setOf()
    println(empty.size == 0) // True
    println(empty.isEmpty()) // True
}
```

**Getting elements at certain positions**

You can think of a list like it is a shelf of an infinite size, where you place the next elements at the next positions. It is important to note that the position of the first element is 0.

![OH7ajUaBQ_6-2o1GgRP-UA_a8aceaece91b401793286b29d20684e1_Shelf.png](Meta%20Android%20Developer%20Coursera%20d4e715a2e3674c5baab68e34e9566bf6/OH7ajUaBQ_6-2o1GgRP-UA_a8aceaece91b401793286b29d20684e1_Shelf.png)

You can get an element at a certain position using box brackets.

```kotlin
fun main() {
    val list = listOf("A", "B", "C")
    println(list[0]) // A
    println(list[1]) // B
    println(list[2]) // C
}
```

**Checking if a list contains an element**

You can check if a set contains a certain element. For that, you can use the **contains** method or the **in** operator. Both of those options return **true** if in the list there is an element equal to the element you are looking for, and it returns **false** otherwise.

```kotlin
fun main() {
    val letters = listOf("A", "B", "C")
    println(list.contains("A")) // true
    println(list.contains("Z")) // false
    println("A" in list) // true
    println("Z" in list) // false
}
```

You can also check the opposite to determine if the collection does not contain the element using the **!in** operator.

```kotlin
fun main() {
    val letters = listOf("A", "B", "C")
    println("A" !in list) // false
    println("Z" !in list) // true
}
```

**Iterating over lists**

You can iterate over a list using a for-loop. Simply place a list on the right side of **in**.

```kotlin
fun main() {
val letters = listOf("A", "B", "C")
    for (letter in letters) {
        print(letter)
    }
}
```

**Using mutable lists**

**List** is a type representing read-only lists. If you want to create a mutable list, use **mutableListOf**, and the result type is **MutableList**. With mutable lists, you can use methods like **add** or **remove** to add or remove a certain element.

```kotlin
fun main() {
    val list = mutableListOf("A", "B")
    list.add("C")
    println(list) // [A, B, C]
    list.remove("B")
    println(list) // [A, C]
}
```

You can also change an element at a certain position using box brackets with index and assignment.

```kotlin
fun main() {
    val list = mutableListOf("A", "B", "C")
    list[1] = "Z"
    println(list) // [A, Z, C]
}
```

### Use a Set

In this reading, you will learn to create a set using the **setOf** function. You will also learn how to add elements to sets and explore how to iterate over a set.

### Set

Sets are quite similar to lists; that’s why similar methods are used to operate on them. However, sets do not treat the order as seriously as lists. Some kinds of sets might not respect it. That is why you cannot get elements by index. Instead, sets require their elements to be unique. You will learn how they do that. But let's start from the beginning, that is, creating a set.

**Creating a set**

You create a set using the **setOf** function, and then you specify the next values using arguments.

```kotlin
fun main() {
    val set = setOf('A', 'B', 'C')
    println(set) // [A, B, C]
}
```

The result type is **Set<T>**, where **T** is the type of elements in this set. Since the above code has a set with char values, the type is **Set<Char>**.

```kotlin
fun main() {
    val set: Set<Char> = setOf('A', 'B', 'C')
    println(set) // [A, B, C]
    val ints: Set<Long> = setOf(1L, 2L, 3L)
    println(ints) // [1, 2, 3]
}
```

**Adding elements to sets**

The easiest way to add elements to sets is by using the plus sign. You can add a single element to a set, or you can add two sets together.

```kotlin
fun main() {
    val set = setOf('A', 'B')
    println(set + 'C') // [A, B, C]
    println(set + setOf('C', 'D')) // [A, B, C, D]
    println(setOf('Z') + set) // [Z, A, B]
}
```

**Establishing the size of a set**

You can always check the number of elements in a set using the **size** property.

```kotlin
fun main() {
    val set = setOf('A', 'B', 'C')
    println(set.size) // 3
}
```

To check if a set is empty, you can compare its size to **0**, or you can use the **isEmpty** method.

```kotlin
fun main() {
    val set = setOf('A', 'B', 'C')
    println(set.size == 0) // false
    println(set.isEmpty()) // false

    val empty: Set<Int> = setOf()
    println(empty.size == 0) // true
    println(empty.isEmpty()) // true
}
```

**Elements in sets are unique**
Elements that are already in a set are not added; their addition is just ignored.

```kotlin
fun main() {
    val set = setOf('A', 'B', 'C')
    println(set + 'B') // [A, B, C]
    println(set + setOf('B', 'D')) // [A, B, C, D]

    val list = listOf('A', 'B', 'C')
    println(list + 'B') // [A, B, C, B]
    println(list + listOf('B', 'D')) // [A, B, C, B, D]
}
```

Also, if you duplicate arguments in the **setOf** function, the second argument will be ignored.

```kotlin
fun main() {
    val set = setOf('A', 'B', 'A')
    println(set) // [A, B]
}
```

Two elements are duplicated if they are equal, so if **==** between them returns **true**. Since regular classes are considered unique, they are never considered to be duplicates.

```kotlin
class User(val name: String)

fun main() {
    val set = setOf(User("A"), User("A"))
    println(set + User("A")) // [User@XXX, User@YYY, User@ZZZ]
}
```

However, data classes are equal when their all-constructor properties have the same values.

```kotlin
data class User(val name: String)

fun main() {
    val set = setOf(User("A"), User("A"))
    println(set + User("A")) // [User(name=A)]
}
```

**Checking if a set contains an element**

You can check if a set contains a certain element. You can use the **contains** method or **in** operator. Both options return **true** if there is an element in the set equal to the element you are looking for, otherwise it returns **false**.

```kotlin
fun main() {
    val letters = setOf('A', 'B', 'C')
    println(set.contains('A')) // true
    println(set.contains('Z')) // false
    println('A' in set) // true
    println('Z' in set) // false
}
```

You can also check the opposite to determine if the set does not contain the element, by using **!in** operator.

```kotlin
fun main() {
    val letters = setOf("A", "B", "C")
    println("A" !in list) // false
    println("Z" !in list) // true
}
```

**Iterating over sets**

You can iterate over a set using a for-loop. Simply place a set on the right side of **in**.

```kotlin
fun main() {
    val letters = setOf('A', 'B', 'C')
    for (letter in letters) {
        print(letter)
    }
}
```

### **Using mutable sets**

**Set** is a type representing read-only sets. If you want to create a mutable set, use **mutableSetOf**, and the result type is **MutableSet**. With mutable sets, you can use methods like **add** or **remove** to add or remove a certain element.

```kotlin
fun main() {
    val set = mutableSetOf('A', 'B')
    set.add('C')
    println(set) // [A, B, C]
    set.remove('B')
    println(set) // [A, C]
}
```

### Map

In this reading, you will learn to create a map using the **mapOf** function. You will also learn how to find a value in a map by using the **key** and you'll explore how to add elements to a map. Lastly, you will learn how to iterate over a map.

Map represents an unordered collection of key-value pairs. Keys are unique and each of them maps to exactly one value. The values can have duplicates. Maps are useful for storing logical connections between objects, for example, an employee's ID and their position.

**Creating maps**

You can create a map using the **mapOf** function and then use key-value pairs as arguments to specify key-value associations. For instance, you might define a map that associates countries with their capitals. Pairs can be defined using a constructor or using the **to** function.

```kotlin
fun main() {
    val capitals = mapOf("USA" to "Washington", "Poland" to "Warsaw", "Ukraine" to "Kyiv")
    //    val capitals = mapOf(
    //        Pair("USA", "Washington"),
    //        Pair("Poland", "Warsaw"),
    //        Pair("Ukraine", "Kyiv")
    //    )
    println(capitals) // {USA=Washington, Poland=Warsaw, Ukraine=Kyiv}
}
```

The result type is **Map<K, V>**, where **K** is the type of a key, and **V** is the type of the value. In the case of capitals, both keys and values are of type **String**, so the map type is **Map<String, String>**. However, it does not need to be the same type.

Consider a map with associations between letters and their positions in the English alphabet, as in the example below. Its type is **Map<Char, Int>**, because its keys are characters, and values are integers.

```kotlin
fun main() {
    val capitals: Map<String, String> =
        mapOf("USA" to "Washington", "Poland" to "Warsaw", "Ukraine" to "Kyiv")

    println(capitals) // {USA=Washington, Poland=Warsaw, Ukraine=Kyiv}

    val alphabet: Map<Char, Int> = mapOf('A' to 1, 'B' to 2, 'C' to 3)

    println(alphabet) // {A=1, B=2, C=3}
}
```

**Finding a value for a key**

To find a value by a key, use a box bracket with the key. For instance, to find a value for the key **A** in the **alphabet** map, use **alphabet['A']**. The result is a nullable value type, so **Int?** in this case.

Why nullable? If the key you asked for is not in the map, then **null** will be returned.

```kotlin
fun main() {
    val alphabet: Map<Char, Int> = mapOf('A' to 1, 'B' to 2, 'C' to 3)
    val number: Int? = alphabet['A']
    println(number) // 1
    println(alphabet['B']) // 2
    println(alphabet['&']) // null
}
```

**Adding elements to a map**

Just like a regular list or a regular set, a regular map is read-only, so it does not have methods that would allow adding or removing elements. However, you can use plus sign to create a new map with new associations. If you add a pair into a map, the result is a map with a new association. If you add a new map, the result is a merge of those two maps.

```kotlin
fun main() {
    val map1 = mapOf('A' to "Alex", 'B' to "Bob")
    val map2 = map1 + ('C' to "Celina")
    println(map1) // {A=Alex, B=Bob}
    println(map2) // {A=Alex, B=Bob, C=Celina}
    val map3 = mapOf('D' to "Daniel", 'E' to "Ellen")
    val map4 = map2 + map3
    println(map3) // {D=Daniel, E=Ellen}
    println(map4) // {A=Alex, B=Bob, C=Celina, D=Daniel, E=Ellen}
}
```

Beware that duplicated keys are not allowed, so when you add a new association, it removes the old one.

```kotlin
fun main() {
    val map1 = mapOf('A' to "Alex", 'B' to "Bob")
    val map2 = map1 + ('B' to "Barbara")
    println(map1) // {A=Alex, B=Bob}
    println(map2) // {A=Alex, B=Barbara}
}
```

You can also remove certain keys from a map using the minus sign.

```kotlin
fun main() {
    val map1 = mapOf('A' to "Alex", 'B' to "Bob")
    val map2 = map1 - 'B'
    println(map1) // {A=Alex, B=Bob}
    println(map2) // {A=Alex}
}
```

**Checking if a map contains a key**

You can check if your map contains a key using the **in** keyword.

```kotlin
fun main() {
    val map = mapOf('A' to "Alex", 'B' to "Bob")
    println('A' in map) // true
    println('Z' in map) // false
}
```

**Checking map size**

You can check how many associations you have in a map using the **size** property.

```kotlin
fun main() {
    val map = mapOf('A' to "Alex", 'B' to "Bob")
    println(map.size) // 2
}
```

**Iterating over maps**

You can iterate over a map using a for-loop. You iterate over entries that contain **key** and **value** properties.

```kotlin
fun main() {
    val map = mapOf('A' to "Alex", 'B' to "Bob")
    for (entry in map) {
        println("${entry.key} is for ${entry.value}")
    }
}

// A is for Alex
// B is for Bob
```

You can also restructure an entry into two variables. Kotlin supports restructuring in a for-loop.

For example:

```kotlin
fun main() {
    val map = mapOf('A' to "Alex", 'B' to "Bob")
    for ((letter, name) in map) {
        println("$letter is for $name")
    }
}
// A is for Alex
// B is for Bob
```

**Mutable map**

You can also create a mutable map using **mapOf** function.

The result type is **MutableMap**. You can add new associations to it using the **put** method or box bracket and assignment. You can also remove an association by key using the **remove** method.

```kotlin
fun main() {
    val map: MutableMap<Char, String> = mutableMapOf('A' to "Alex", 'B' to "Bob")
    map.put('C', "Celina")
    map['D'] = "Daria"
    println(map) // {A=Alex, B=Bob, D=Daria, C=Celina}
    map.remove('B')
    println(map) // {A=Alex, D=Daria, C=Celina}
}
```