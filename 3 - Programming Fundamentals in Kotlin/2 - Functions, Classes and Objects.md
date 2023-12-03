## Functions, classes and objects

### Variable Scope & Local Functions

### Variable scope

Inside of functions, it is possible for variables to be defined. These variables are called local variables, and they are visible only in their definition scope: the braces inside which they are defined. If you have a function, **f1**, that calls a function, **f2**, each can have its own local variable. However, these variables can only be used at the function in which they are defined.

```kotlin
fun f1() {
    val a = "Text 1"
    println(a) // can use a here
    // here, I cannot use b
}

fun f2() {
    val b = "Text 2"
    f2()
    println(b) // can use b here
    // here, I cannot use a
}

fun main() {
    f2()
    // here, I cannot neither use a or b
}
```

Scope limitations are very important for building independence between functions. Local variables should stay local, and other functions should not take an interest in them.

If you want to define a variable that can be used by multiple functions, you need to define it in a wider scope. As mentioned already, a simple heuristic is that each variable is visible in the scope where it is defined. To make a variable that can be used by multiple functions, define it at the same level as those functions. In the code below, a variable is defined outside all functions. Such variables are known as top-level variables. Then inside **setName** the value is set to **"Mike"**, and inside **printName** the current name is printed. As a result, the below code will print **"Mike"**.

```kotlin
var name = ""

fun setName() {
    name = "Mike"
}

fun printName() {
println(name)
}

fun main() {
setName()
printName()
}
```

### Local functions

Just as local variables can be defined, so too can local functions. This is what functions defined inside other functions are called. Just like local variables, they can only be used in the scope of their definition. So, at the same function and after their definition. Top-level functions do not have such limitations - they can be used everywhere, even in functions defined earlier in the file.

```kotlin
fun b() {
    // here I cannot use function a
}

fun main() {
    // here I cannot use function a
    fun a() {
println("A")
    }
a() // Here I can use function a
b()
c()
a() // Here I can use function a
}

fun c() {
    // here I cannot use function a
}
```

### Functions with Parameters

Functions with parameters are very important and popular in programming. Let's examine a few examples based on what you've learned in the course so far.

In an earlier reading, you learned to print a triangle made up of stars.

```kotlin
fun main() {
    val height = 5
    for (i in 1..height) {
        for (j in 1..i) {
            print("*")
        }
        println()
    }
}
```

```kotlin
*
**
***
****
*****
```

You could, however define it more easily with functions. First, you need a function to print a line with a certain number of stars. Let's call it **printStars**, and it should have a parameter that will be used to specify the number of stars. Such a function would be useful not only for this but also for most other triangles.

```kotlin
fun printStars(num: Int) {
    for (j in 1..num) {
        print("*")
    }
    println()
}

fun main() {
    val height = 5
    for (i in 1..height) {
        printStars(i)
    }
}
```

Now, you can extract a function to draw the whole ascending triangle.

```kotlin
fun printStars(num: Int) {
    for (j in 1..num) {
        print("*")
    }
    println()
}

fun ascendingTriangle(height: Int) {
    for (i in 1..height) {
        printStars(i)
    }
}

fun main() {
    ascendingTriangle(5)
}
```

You could do the same to define the descending triangle. What is more, by connecting both functions, you can print an isosceles triangle.

```kotlin
fun printStars(num: Int) {
    for (j in 1..num) {
        print("*")
    }
    println()
}

fun ascendingTriangle(height: Int) {
    for (stars in 1..height) {
        printStars(stars)
    }
}

fun descendingTriangle(height: Int) {
    for (stars in height downTo 1) {
        printStars(stars)
    }
}

fun isoscelesTriangle(width: Int) {
    ascendingTriangle(width - 1)
    descendingTriangle(width)
}

fun main() {
    println("Ascending triangle:")
    ascendingTriangle(5)
    println("Descending triangle:")
    descendingTriangle(5)
    println("Isosceles triangle:")
    isoscelesTriangle(5)
```

**Ascending triangle**

```kotlin
*
**
***
****
*****
```

**Descending triangle**

```kotlin
*****
****
***
**
*
```

Isosceles **triangle**

```kotlin
*
**
***
****
*****
****
***
**
*
```

### Functions with return

Functions can also return a value. For that, a function should declare the return type, using a colon and type after the parameters parenthesis. Inside a body, such a function should also use **return** to return the value.

Here is a definition of **triangleArea**. It's a function that calculates the area of a triangle with a certain width and height. Its result is of type **Double**, so you can place the function call on the right side of the value assignment. Once this function returns a value, it is assigned to the variable, and you can use it later.

```kotlin
fun triangleArea(width: Double, height: Double): Double {
    return width * height / 2
}

fun main() {
    val area: Double = triangleArea(1.0, 2.0)
    println(area) // 1.0
    println(triangleArea(2.0, 2.0)) // 2.0
    println(triangleArea(5.0, 5.0)) // 12.5
    println(triangleArea(10.0, 20.0)) // 100.0
}
```

Let's now implement the **biggerOf** function so that out of two arguments, it returns the largest one. You could implement it using an **if-else** statement, with **return** in each branch.

```kotlin
fun biggerOf(a: Int, b: Int): Int {
    if (a > b) {
        return a
    } else {
        return b
    }
}

fun main() {
    println(biggerOf(3, 1)) // 3
    println(biggerOf(10, 20)) // 20
}
```

Such a function could be simplified by using **if-else** as an expression, but that's not the point. Notice that in this case, you specify **return** two times: one for each possible branch of condition.

### Unreachable code after return

Using the **return** keyword immediately ends a function call, so whatever is placed after it won't be called. Let's say that you modify **triangleArea** by adding a **print** call after **return**. Does it change anything? No, it does not! Once **return** is called, the function is finished, so this **return** is unreachable.

```kotlin
fun triangleArea(width: Double, height: Double): Double {
    return width * height / 2
    println("Will never be called")
}

fun main() {
    println(triangleArea(10.0, 20.0)) // 100.0
}
```

That also means that in the **biggerOf** implementation, you do not need an **else** block. You could also implement it in the following way:

```kotlin
fun biggerOf(a: Int, b: Int): Int {
    if (a > b) {
        return a
    }
    return b
}

fun main() {
    println(biggerOf(3, 1)) // 3
    println(biggerOf(10, 20)) // 20
}
```

The behaviour of **biggerOf** stayed the same. If **a** is greater than **b**, than **a** will be returned, and the function will be finished. Otherwise, **b** will be returned.

### Single-expression functions

Often, developers define functions just to return a processed value. Both **triangleArea** and **biggerOf** are great examples. Such functions can be recognized by the **return** keyword used in the first line. That means the whole body is just a single expression.

```kotlin
fun triangleArea(width: Double, height: Double): Double {
    return width * height / 2
}

fun biggerOf(a: Int, b: Int): Int {
    return if (a > b) a else b
}
```

In Kotlin, there is a special syntax for single expression functions. Instead of braces with the body, you use the equality sign, which specifies what should be returned.

```kotlin
fun triangleArea(width: Double, height: Double): Double = width * height / 2

fun biggerOf(a: Int, b: Int): Int = if (a > b) a else b
```

Such notation is shorter, but you won't really encounter it in the course because it can be overly complicated. But you need to be aware that single-expression functions exist because they are popular in professional projects.

Single-expression functions are nothing new, they are just a simpler notation for functions. Here is how you can understand them:

```kotlin
fun {function name}({parameters}): {result type} = {expression body}

// is equivalent to 

fun {function name}({parameters}): {result type} {
    return {expression body}
}
```

For instance:

```kotlin
fun triangleArea(width: Double, height: Double): Double = width * height / 2

// is equivalent to

fun triangleArea(width: Double, height: Double): Double {
    return width * height / 2
}
```

### Recursion

In this reading, you will learn more about recursion and recursive functions.

### Recursion

Let's say that you need to implement a function that calculates the factorial of a number. Factorial, in mathematics, is the product of all positive integers less than or equal to a given positive integer.

For instance, a factorial of 4 is 1∗2∗3∗4=241∗2∗3∗4=24 .

One way of implementing such a function is using a **for loop**.

You might define a variable called **accumulator**, with an initial value of 1, that will be used to accumulate all the numbers.

Then, for each number from 1 to the number you calculate factorial of, you will modify the value by multiplying it by the next number.

After that, all you need to do is to return the **accumulator** variable.

```kotlin
fun factorial(number: Int): Int {

    var accumulator = 1

    for (i in 1..number) {

        accumulator = accumulator * i
    }

    return accumulator
}

fun main() {

    println(factorial(1)) // 1
    println(factorial(2)) // 2
    println(factorial(3)) // 6
    println(factorial(4)) // 24
    println(factorial(5)) // 120
    println(factorial(6)) // 720
}
```

That is a perfectly valid implementation of factorial.

To understand it, let's first observe how the results of the function **factorial** are connected to one another.

![Ekran Resmi 2023-11-28 12.03.03.png](Meta%20Android%20Developer%20Coursera%20d4e715a2e3674c5baab68e34e9566bf6/Ekran_Resmi_2023-11-28_12.03.03.png)

Notice that the factorial of each number is equal to the factorial of the previous one, multiplied by the number its factorial of:

**factorial(n) = factorial(n - 1) * n**

That is true for all numbers, except for 1, whose factorial is 1:

**factorial(1) = 1**

You can also assume that the factorial of all the numbers smaller than 1 is 0.

Keeping all that in mind, you can implement the factorial function in the following way:

```kotlin
fun factorial(number: Int): Int {

    if (number <= 1) {
        return 1
    }
    return factorial(number - 1) * number
}

fun main() {
    println(factorial(1)) // 1
    println(factorial(2)) // 2
    println(factorial(3)) // 6
    println(factorial(4)) // 24
    println(factorial(5)) // 120
    println(factorial(6)) // 720
}
```

This implementation is very different from the previous one, but it gives the same results.

This implementation of the **factorial** function achieves that by calling itself. Functions that call themselves are called **recursive functions**. Let's analyze how it works step by step.

Let's say that you call **factorial(3)**. The steps for this call are broken down as follows:

**Step 1:** Run the factorial function with 3 as the number. ****Since **3** is larger than **1**, you pass the condition and reach **factorial(2) * 3**.

So, you need to calculate the value of **factorial(2)**.

**Step 2:** Run the factorial function with **2** as the number. ****Since **2** is larger than **1**, you pass the condition and reach **factorial(1) * 2**.

So, you need to calculate **factorial(1)**.

**Step 3:** Run the factorial function with **1** as the number. ****Since **1** is not larger than **1**, it returns **1**.

So **factorial(1) * 2** becomes **1 * 2** which becomes **2**.

As the resulting **factorial(2) * 3** becomes **2 * 3,** that becomes **6**.

So that is the result of **factorial(3)**.

Think of the calculation and method calls running like the example below.

```kotlin
factorial(3) ->
(factorial(2) * 3) ->
((factorial(1) * 2) * 3) ->
((1 * 2) * 3) ->
(2 * 3) ->
6
```

Notice that it is very important that our function starts with a condition so that after a limited number, recursive calls will not be fulfilled. Such a condition (or its result) is known as the base case. Without it, recursive calls will happen until the program is stopped by too many recursive calls.

The recursive approach is just another way a function can be implemented. Sometimes it can make our code simpler, but, in most cases, it's just another method with no clear advantages. Often, most developers prefer the classical approach (known as iterative), but it is worth knowing both options.

### Default & Named Arguments

### Default arguments

One very useful Kotlin possibility is to define default arguments. For example, imagine that you implement a function to open a web browser. However, browsers can be opened in normal or incognito mode, so, in your function definition, you should have a parameter that specifies which mode should be used.

```kotlin
fun openBrowser(url: String, incognitoMode: Boolean) {

    println("Opening $url" + if (incognitoMode) " in incognito mode" else "")

    // ...

}

// Usage

fun main() {

    openBrowser("website1.com", false) // Opening website1.com

    openBrowser("website2.com", false) // Opening website2.com

    openBrowser("website3.com", true) // Opening website3.com in incognito mode
}
```

However, in most cases, you do not want this function to specify **false** for incognito mode. It should be used by default. To make that possible, you should specify the default value after the parameter definition.

```kotlin
fun openBrowser(url: String, incognitoMode: Boolean = false) {

    println("Opening $url" + if (incognitoMode) " in incognito mode" else "")

    // ...

}

// Usage

fun main() {

    openBrowser("website1.com") // Opening website1.com

    openBrowser("website2.com") // Opening website2.com

    openBrowser("website3.com", true) // Opening website3.com in incognito mode
}
```

You can specify default arguments for all the positions you want. Here is an example function with default arguments for both its parameters of type **String**.

```kotlin
fun cheer(how: String = "Hello, ", who: String = "World") {

    print("$how $who")
}

fun main() {

    cheer() // Hello, World

    cheer("Hi ") // Hi World

    cheer("Hi ", "Learner") // Hi Learner
}
```

Although you can specify arguments for whatever parameter positions you want, you might be wondering what you can do if you only want to specify the argument for the **who** parameter. This parameter is at the second position, so to specify it without specifying the arguments for the previous positions, you need to use named arguments.

### **Named arguments**

When you call a function inside a parenthesis, you can specify arguments according to the order of the parameters that are associated. That's the default way of calling a function, but there is also another option: for each argument, you can explicitly specify what parameter is associated. You do that by introducing parameter names and the equal sign in front of a parameter. When you do that, arguments do not need to be in parameter order.

```kotlin
fun cheer(how: String = "Hello, ", who: String = "World") {

    print("$how $who")
}

fun main() {

    cheer(how = "Hi ") // Hi World

    cheer(who = "Learner") // Hello, Learner

    cheer(how = "Hi ", who = "Learner") // Hi Learner

    cheer(who = "Learner", how = "Hi ") // Hi Learner
}
```

The primary reason for using named arguments is to improve readability – you explicitly state what the meaning of an argument is when it might not be obvious to the person reading your code. The other reason to use it is when you want to specify arguments for parameters at further positions without specifying arguments for the earlier position. For example, when you call **cheer(who = "Learner")**, you specify **who** without specifying **how**.

### P**roperties & Primary Constructor**

### Modeling the world

In programming, programmers often try to model the real world. For that, classes with properties that express whatever is important in a system are used.

Let's say you implement a system to manage a school.

When you think about a school, you may think about students, teachers, subjects and so on. It's convenient to represent them in your system by using classes.

```kotlin
class Student

class Teacher

class Subject
```

For those classes, you should specify properties. In your system, you do not need to know everything about each person, only what is relevant to the system. So, you should specify only the data that is necessary for the program to work correctly.

For example, a subject might be defined by the name of the teacher who is teaching it. For a teacher, it might be: name, surname, birthday and work status. Of course, those properties might be completely different in a different system. Let's assume that your system sends greetings for teachers' birthdays, and that is why you need the **birthday** property, but in other systems, you might not be interested in keeping such a value.

```kotlin
class Subject(
    val name: String,
    val teacher: Teacher,
    val isObligatory: Boolean,
)

class Teacher(
    val name: String,
    val surname: String,
    val birthday: String,
    val status: String,
)

fun main() {
    // I use named arguments convention here
    val remigiuszFrost =
        Teacher(name = "Remigiusz", surname = "Frost", birthday = "23.07.1987", status = "ACTIVE")
    val biology1 = Subject(name = "Biology 1", teacher = remigiuszFrost, isObligatory = true)
    println(biology1.isObligatory) // true
    println(biology1.teacher.birthday) // 23.07.1987
    println(biology1.teacher.status) // ACTIVE
}
```

Notice that in the above example, in the class **Subject** you keep the property type **Teacher**. That's a popular practice - now someone who has access to an object of type **Subject** can also read the properties of the teacher teaching this subject.

Every additional property in a class is a cost - the value for those properties needs to be collected, stored and maintained (as a status can change). That is why you should try to limit the number of properties in your classes to the minimum required by your system.

Nevertheless, complex systems tend to grow over time, and their object can also have a lot of properties, all required by the functionalities of this system. It is hard to work on such systems, considering how hard it is to create an instance of a class that has over 20 properties. In some systems, it cannot be avoided, but you can try to postpone it by limiting the number of properties at the start.

### The **id** property

In real-life systems, classes often have a property called **id**. Let's consider the class below:

```kotlin
class Student(
    val id: Int,
    val name: String,
    val surname: String,
)
```

The **id** property uniquely identifies a user.

Let's say you have two users with the same name and surname, and one of them got a bad grade. If you associate this grade with the student's name and surname, it might be associated with the incorrect person. That's why you use student id instead. Because it's unique, you eliminate the risk of making a mistake.

```kotlin
class Grade(val points: Int, val studentId: Int, val topicId: Int)

class Student(
    val id: Int,
    val name: String,
    val surname: String,
)
```

### Methods

### Receiver

If you want to call a method, you need to have an object. You can then call this method on an object.

For instance, when you have a class **Dog** with a method **feed**, to call this method outside the class, you need to first have an object of type **Dog**.

```kotlin
class Dog(val name: String) {

    var hunger = 62

    fun feed() {

        println("Feeding $name")

        hunger = 0
    }
}

fun main() {

    val dog = Dog("Rex")

    dog.feed() // Feeding Rex
}
```

Notice that an instance of type **Dog** is a part of the **feed** method call. Inside the method, you use the **name** and **hunger** properties from the object that was used during the call. In a way, it is similar to defining **feed** as a top-level function and passing **Dog** as an argument:

```kotlin
class Dog(val name: String) {

    var hunger = 62
}

fun feed(dog: Dog) {

    println("Feeding ${dog.name}")

    dog.hunger = 0
}

fun main() {

    val dog = Dog("Rex")

    feed(dog) // Feeding Rex
}
```

The essential difference is that in methods, you access class members implicitly, so, for instance, using just **name**, not **dog.name**. How does it work?

When you call a method, the object of their class is passed to their body. It is called a **receiver**. It can be accessed using **this** keyword, also known as **receiver reference**. So, if you want to reference an object used to call a method inside this method, use the **this** keyword.

```kotlin
class Dog(val name: String) {

    var hunger = 62

    fun feed() {

        val currentDog: Dog = this

        println("Feeding ${currentDog.name}")

        currentDog.hunger = 0
    }
}

fun main() {

    val dog = Dog("Rex")

    dog.feed() // Feeding Rex
}
```

When you call methods or properties inside methods, such as when you call **name**, you are calling methods or properties on the receiver, so it's like calling **this.name**.

```kotlin
class Dog(val name: String) {

    var hunger = 62

    fun feed() {

        println("Feeding ${this.name}")

        this.hunger = 0
    }
}

fun main() {

    val dog = Dog("Rex")

    dog.feed() // Feeding Rex
}
```

However, there is a rule in most programming languages that methods or properties can be called on **this** explicitly, so **this.** can generally be skipped. However, sometimes you may want to use **this** explicitly.

One example might be when you have a method parameter and class property with the same name. Like in the below class, there is a property **name** and a method **changeName** with a parameter **name**. So, if you use **name** inside the class, you will have a value of the parameter. To access the property, use **this.name**.

```kotlin
class User(var name: String) {

    fun changeName(name: String) {

        println("Changed name from ${this.name} to $name")

        this.name = name
    }
}

fun main() {

    val user = User("Alpha") // Changed name from Alpha to Beta

    user.changeName("Beta") // Beta

    println(user.name)
}
```

### Methods on String

Previously, you may have observed some methods defined on **String**. Let's review them:

- **uppercase** returns the same text, but with all characters in uppercase.
- **lowercase** returns the same text, but with all characters in lowercase.
- **replace** changes all the repetition of one string into another.

```kotlin
fun main() {

    val text = "Some Text"

    println(text.uppercase()) // SOME TEXT

    println(text.lowercase()) // some text

    println(text.replace("Text", "NewText")) // Some NewText

    println("A B A C".replace("A", "G")) // // G B G C
}
```

### Conversion methods

Other basic types have many useful methods, starting from the methods used to convert from one type to another. All the numbers can be transformed into other basic types of numbers using methods starting from to and ending with the name they should be transformed to. For instance, to transform **Int** or **Long** to **Float**, use **toFloat()** as in the example below.

```kotlin
fun main() {

    val i: Int = 10

    val l: Long = i.toLong()

    val f1: Float = i.toFloat()

    val f2: Float = l.toFloat()

    println(f1) // 10.0

    println(f2) // 10.0
}
```

### Interfaces

In this reading, you will learn the relationship between types and learn to use **is check** and **as** casting.

When you define a class **Dog**, as a result, you also create a **type** called **Dog**, which is a group that accepts only objects created using the **Dog** class.

```kotlin
class Dog

fun main() {
    val dog: Dog = Dog()
}
```

When you define an interface called **Animal**, you specify a type that accepts all the objects that implement this interface. It also accepts **Dog** if it implements **Animal**. All the objects of type **Dog** can be used as **Animal**, but not the other way around.

```kotlin
interface Animal

class Dog : Animal

fun main() {
    val dog: Dog = Dog()
    val animal: Animal = dog
    val dog2: Dog = animal // ERROR!!!
}
```

You can say that **Dog** is a subtype of **Animal**. You can also say that **Animal** is a supertype of **Dog**.

![vDUHN9aJQaa1BzfWibGmAA_e7c369b386bd4496b7b4133b39debbe1_Animal.png](Meta%20Android%20Developer%20Coursera%20d4e715a2e3674c5baab68e34e9566bf6/vDUHN9aJQaa1BzfWibGmAA_e7c369b386bd4496b7b4133b39debbe1_Animal.png)

Using an object of some type where its subtype is expected is called **up-casting**. The name comes from how the relationships between types are viewed. It is a hierarchical structure where some types are above others. The more abstract types are above the less abstract types. Since every **Dog** is an **Animal**, but not the other way around, you typically present **Animal** above **Dog**. You also add an arrow from **Dog** to **Animal**. That means you can use **Animal** as a **Dog**, but not the other way around.

In an earlier module, you learned about **Number**. It is an interface implemented by all the classes representing numbers, like **Int**, **Long**, **Float** or **Double**. There is also **Any**, which is a supertype of all the mentioned types.

![gFtj__hzQRybY__4c1Ecqg_594cbf20fcb5481c93d7ec44b4d4ace1_Any-number.png](Meta%20Android%20Developer%20Coursera%20d4e715a2e3674c5baab68e34e9566bf6/gFtj__hzQRybY__4c1Ecqg_594cbf20fcb5481c93d7ec44b4d4ace1_Any-number.png)

You can always use a subtype, where its supertype is expected.

```kotlin
fun consumeAny(any: Any) {}

fun consumeNumber(number: Number) {}

fun main() {
    val i: Int = 120
    val l: Long = 1234567890L
    val d: Double = 10.0
    consumeAny(i) // upcasting Int to Any
    consumeAny(l) // upcasting Long to Any
    consumeAny(d) // upcasting Double to Any
    consumeNumber(i) // upcasting Int to Number
    consumeNumber(l) // upcasting Long to Number
    consumeNumber(d) // upcasting Double to Number
}
```

Does it work the other way around? Let's say that you have a variable of type **Animal**. Can you turn it into **Dog**?

Such an operation would not be safe. **Animal** can be of type **Dog**, but it can also be of type **Cat**. While it is possible, it is called **down-casting**, and it is done by using the **as** keyword, and the type you want to cast to. However, think twice before you use it, because if you cast into an incorrect type, an exception will break your program.

```kotlin
interface Animal

class Dog(val name: String) : Animal {
    fun retrieve(item: String) {
        println("Retrieving $item")
    }
}

class Cat : Animal

fun play(animal: Animal) {
    val dog: Dog =
        animal as Dog // Do that ONLY when you know an object is of the type you are casting to
    dog.retrieve("stick")
}

fun main() {
    play(Dog("Rex")) // Retrieving stick
    play(Cat("Garfield")) // ERROR!
}
```

There is also a safer variant. You can check if an object is of a particular type using the **is** keyword. So to check if **Animal** is **Dog**, you can use **animal is Dog**, which returns **true** if it is, and **false** otherwise.

```kotlin
interface Animal

class Dog(val name: String) : Animal {
    fun retrieve(item: String) {
        println("Retrieving $item")
    }
}

class Cat(val name:String) : Animal

fun checkIsDog(animal: Animal) {
    if (animal is Dog) {
        println("It is a dog")
    } else {
        println("It is not a dog")
    }
}

fun main() {
    checkIsDog(Dog("Rex")) // It is a dog
    checkIsDog(Cat("Garfield")) // It is not a dog
}
```

After you checked if **animal is Dog**, inside the body of such a condition, **animal** must be of type **Dog**. It is because if it is not, then the condition would not pass. Kotlin knows that, and so it changes the type in the process called **smart-casting**. This way, using smart-casting, you can safely **down-cast** objects for some scope.

```kotlin
interface Animal

class Dog(val name: String) : Animal {
    fun retrieve(item: String) {
        println("Retrieving $item")
    }
}

class Cat : Animal

fun play(animal: Animal) {
    if (animal is Dog) {
        animal.retrieve("stick")
    } else {
        println("I do not know how to play with this animal")
    }
}

fun main() {
    play(Dog("Rex")) // Retrieving stick
    play(Cat("Garfield")) // I do not know how to play with this ani
```

Often smart-casting is used together with a **when** statement.

```kotlin
interface Animal

class Dog(val name: String) : Animal {
    fun retrieve(item: String) {
        println("Retrieving $item")
    }
}

class Cat : Animal {
    fun pet() {
        println("Mrr")
    }
}

fun play(animal: Animal) {
    when (animal) {
        is Dog -> animal.retrieve("stick")
        is Cat -> animal.pet()
    }
}

fun main() {
    play(Dog("Rex")) // Retrieving stick
    play(Cat("Garfield")) // Mrr
}
```

### Inheritance

### Parent-child relationship

When one class inherits from another, it takes all the previous class’s behavior (its methods and properties). It also becomes its subclass, which means that it can be used wherever its parent is expected. So, in the example below, **Dog** is a subclass of **Mammal**, or **Mammal** is a superclass of **Dog**. It is also called a parent-child relationship, so **Dog** is a child of **Mammal**, and **Mammal** is a parent of **Dog**.

```kotlin
open class Mammal {
    fun feedChildren() {}
}
class Dog: Mammal {
    fun fetchStick() {}
}

fun feed(mammal: Mammal) {
    mammal.feedChildren()
}

fun main() {
    val dog = Dog()
    dog.feedChildren()
    dog.fetchStick()
    feed(dog)
}
```

### Calling superclass constructor

When you create an instance of a class, you need to call its constructor. When a class **Dog** has a constructor that expects **name**, when you create an instance of this class, you need to specify a value for this parameter.

```kotlin
class Dog(val name: String)

fun main() {
    val dog = Dog("Rex") // some string must be here
    println(dog.name) // Rex
}
```

When a class is inherited from another class it takes all the behavior of the parent class. That includes its constructor properties, but to initialize them with some values, the parents' constructor needs to be called. That means, when you call a constructor of a subclass, it also needs to call its parent constructor. How is this done? When you specify a class that you inherit from, you also need to call the constructor of this class.

```kotlin
open class Dog(val breed: String)

class Labrador(val name: String) : Dog("Labrador Retriever") // Here we call animals' constructor

fun main() {
    val lab = Labrador("Coco")
    println(lab.name) // Coco
    println(lab.breed) // Labrador Retriever
}
```

When calling the parent constructor, you can use constructor parameters. What is important, they do not need either val or var for that.

Let's consider the following case: Assume that our Dog class has a constructor property name. Dog has a subclass [Labrador.name](http://labrador.name/) might be different for each dog, so it should be specified when a constructor is called. How can you do that?

One way is that inside the Labrador constructor, you define a val property name, however since such a property is already defined in the parent:

1. The property name inside Dog must be open (must have open modifier)
2. You must add override in front of the property definition in Labrador

```kotlin
open class Dog(open val name: String)

class Labrador(override val name: String) : Dog(name)

fun main() {
    val lab = Labrador("Coco")
    println(lab.name) // Coco
}
```

However, there is also a much easier option. Inside **Labrador** you can define **name** without **val**. In such a case, **Labrador** does not define **name** property, but it does not need to - it is already defined by its parent. The **name** parameter can be passed to the superclass constructor, and both classes behave practically the same as in the previous example.

```kotlin
open class Dog(val name: String)

class Labrador(name: String) : Dog(name)

fun main() {
    val lab = Labrador("Coco")
    println(lab.name) // Coco
}
```

### Visibility Modifiers

Encapsulation, a fundamental concept in modern programming, involves restricting access to certain properties and methods of a class to ensure controlled interactions. When designing a class, such as one representing a bank account, developers must carefully consider what functionalities they want to expose and what they want to keep hidden. Visibility modifiers play a crucial role in achieving encapsulation by determining the scope of access to different elements within a class or across files and modules.

The primary visibility modifier is "private," which, when applied to a property or function, confines its usage to the class where it is defined. This is essential for hiding sensitive information, like a bank account balance, from external access. In the case of a class representing a bank account, methods like "deposit" and "withdraw" may be designated as public, allowing external interaction, while the "balance" property is marked as private to prevent unauthorized modifications.

Defaulting to "public," elements marked with this modifier are accessible from anywhere in the codebase. Conversely, "private" limits access to the immediate class scope, preventing external use. This can be extended to file-level scope, where the modifier restricts access to the same file, emphasizing the importance of controlled visibility even within a codebase.

Beyond "private," two other significant visibility modifiers are "protected" and "internal." "Protected" is particularly useful inside classes that are either "open" or "abstract." This modifier allows an element to be visible not only within the class it is defined but also in its subclasses. This facilitates controlled access within a class hierarchy, ensuring that certain properties or methods are available for modification within the hierarchy but not externally.

The "internal" modifier expands visibility to the entire module, often corresponding to a project. While it may seem similar to "public" within the project, its significance becomes apparent when dealing with external dependencies. When using libraries or dependencies, encountering elements marked as "internal" signals that these elements are inaccessible to the user and are intended for internal use by the library developers. This highlights the importance of understanding visibility modifiers when incorporating external code into a project.

In practice, developers can strategically use visibility modifiers—private, protected, and internal—to tailor the accessibility of properties and methods based on specific requirements. Encapsulation, achieved through these modifiers, ensures that the internal workings of a class remain hidden and only essential functionalities are exposed, contributing to code robustness, maintainability, and security.

### **Abstract**

When you use the **abstract** keyword before a class definition, you make this class abstract. Abstract classes can be thought of as a hybrid of an open class and an interface. There are two main consequences of making a class abstract:

1. Abstract classes can have abstract methods or properties. Such elements are marked with an **abstract** modifier, and they do not have a body. They are just definitions, similar to those in interfaces, that need to be overridden in subclasses.
2. Abstract classes cannot be used to create objects. However, you can inherit subclasses from them. This is a result of the first consequence - you cannot create objects with abstract methods or properties. Those need to be overridden.

You can use abstract classes as a replacement for interfaces, but this is considered a bad practice. Wherever possible, the preference is to use interfaces. Each class can inherit from only one class but implement many interfaces. Interfaces are considered to be an easier concept to learn compared to abstract classes. The key advantage of abstract classes is that they can have non-open methods (on interfaces, all elements are open) and non-abstract properties.

### **Example of interface code**

```kotlin
interface I
    {
        val a: Int = 123 // ERROR! You cannot define non-abstract properties in Interfaces
    }
```

Abstract classes are mainly used when you want to specify a set of generic operations for multiple classes. Let's say that you write an application that draws various shapes in different ways. You might be drawing them on native Android components,  on websites, or on a terminal. Since you draw in different ways on each of those platforms, you need separate classes.

However, there is also another option. Because a  square and a rectangle can be drawn using lines, you can define an abstract class **ShapeDrawer**, that will define methods **drawSquare** and **drawRectangle** based on the abstract method **drawLine**. Now your drawer classes can inherit from **shapeDrawer** and only need to define one function **drawLine**, to have also **drawSquare** and **drawRectangle**.

Consider for a moment the code for this Abstract class example.

### **Example of Abstract class**

```kotlin
abstract class ShapeDrawer { 
    fun drawSquare(){ 
drawLine() 
    } 
    fun drawRectangle(){ 
        drawLine() 
    } 
    internal abstract fun drawLine() 
} 
class AndroidShapeDrawer():ShapeDrawer(){ 

    override fun drawLine() { 
        //code that draw lines for android platform 
        println("Test code -Draw line for  android platform") 
    } 
} 
class DesktopShapeDrawer():ShapeDrawer(){ 
    override fun drawLine() { 
        //code that draw lines for android platform 
        println("Test code -Draw line for  desktop platform") 
    } 
} 
fun main(){ 
    val androidDrawer:ShapeDrawer = AndroidShapeDrawer() 
    androidDrawer.drawSquare() 
    val desktopDrawer:ShapeDrawer = DesktopShapeDrawer() 
    desktopDrawer.drawSquare() 
}
```

The code produces this output:

![I8GUtwDhThSBlLcA4a4UQA_82a772f10553464682c089928c8f5de1_abstractClassOuotput001.png](Meta%20Android%20Developer%20Coursera%20d4e715a2e3674c5baab68e34e9566bf6/I8GUtwDhThSBlLcA4a4UQA_82a772f10553464682c089928c8f5de1_abstractClassOuotput001.png)

### Interface versus Abstract class

To summarize the difference between Interface and Abstract class:

| Interface | Abstract class |
| --- | --- |
| All methods are open | Methods can be open or non open |
| Methods and members are abstracted by default | Methods and members can be abstract or non abstract |
| A class can implement one or more interface | A class can only be inherited  from one class |

### Define & Use Abstract Classes

In the previous reading, we looked at what an abstract class means and how it works. The code snippet below shows a general format of abstract classes.

```kotlin
abstract class SomeAbstractClass {
    abstract fun abstractMethod()
    fun callAbstractTwice() {
        abstractMethod() // You can use abstract methods inside the class, because it is assumed they
        // will be overridden in the child class.
        abstractMethod()
    }
}

class SomeRegularClass : SomeAbstractClass {
    override fun abstractMethod() {
        println("Calling abstract method")
    }
}

fun main() {
    val regular = SomeRegularClass()
    regular.abstractMethod() // Calling abstract method
    regular.callAbstractTwice()
    // Calling abstract method
    // Calling abstract method
}
```

### Use-case example of abstract classes

In the following example, there are three classes; **AndroidShapeDrawer**, **WebsiteShapeDrawer** and **TerminalShapeDrawer**. Each class has a function to draw a line, draw a square and draw a rectangle.

```kotlin
class AndroidShapeDrawer {
    fun drawLine(fromX: Int, fromY: Int, toX: Int, toY: Int) {
        /*...*/
    }
    fun drawSquare(x: Int, y: Int, size: Int) {
        /*...*/
    }
    fun drawRectangle(x: Int, y: Int, height: Int, width: Int) {
        /*...*/
    }
}

class WebsiteShapeDrawer {
    fun drawLine(fromX: Int, fromY: Int, toX: Int, toY: Int) {
        /*...*/
    }
    fun drawSquare(x: Int, y: Int, size: Int) {
        /*...*/
    }
    fun drawRectangle(x: Int, y: Int, height: Int, width: Int) {
        /*...*/
    }
}

class TerminalShapeDrawer {
    fun drawLine(fromX: Int, fromY: Int, toX: Int, toY: Int) {
        /*...*/
    }
    fun drawSquare(x: Int, y: Int, size: Int) {
        /*...*/
    }
    fun drawRectangle(x: Int, y: Int, height: Int, width: Int) {
        /*...*/
    }
}
```

Each class could implement these functions individually, however, there is another option.

Since **square** and **rectangle** can be drawn using lines, you can define an abstract class **ShapeDrawer**, that will define methods **drawSquare** and **drawRectangle** based on the abstract method **drawLine**. Now our drawer classes can inherit from **ShapeDrawer** and only need to define one function **drawLine** but will also have the functionality **drawSquare** and **drawRectangle**.

```kotlin
abstract class ShapeDrawer {
 
    abstract fun drawLine(fromX: Int, fromY: Int, toX: Int, toY: Int)
 
    fun drawSquare(x: Int, y: Int, size: Int) {
        drawLine(x, y, x + size, y)
        drawLine(x + size, y, x + size, y + size)
        drawLine(x, y, x, y + size)
        drawLine(x, y + size, x + size, y + size)
    }
 
    fun drawRectangle(x: Int, y: Int, height: Int, width: Int) {
        drawLine(x, y, x + width, y)
        drawLine(x + width, y, x + width, y + height)
        drawLine(x, y, x, y + height)
        drawLine(x, y + height, x + width, y + height)
    }
}
 
 
class AndroidShapeDrawer: ShapeDrawer() {
    override fun drawLine(fromX: Int, fromY: Int, toX: Int, toY: Int) { /*...*/ }
}
 
class WebsiteShapeDrawer: ShapeDrawer() {
    override fun drawLine(fromX: Int, fromY: Int, toX: Int, toY: Int) { /*...*/ }
}
 
class TerminalShapeDrawer: ShapeDrawer() {
    override fun drawLine(fromX: Int, fromY: Int, toX: Int, toY: Int) { /*...*/ }
}
```

This is how abstract classes are used in practice - to share behavior for all its subclasses and allow subclasses to focus on their class-specific functionality.