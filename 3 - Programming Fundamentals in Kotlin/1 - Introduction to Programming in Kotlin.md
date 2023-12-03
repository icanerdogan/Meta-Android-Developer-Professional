## Introduction to Programming in Kotlin

### Variables

### What are variables?

Since a variable is an alternative name for a value, when you place another variable on the right side of a value assignment, the value of the variable is assigned, not the variable itself. For example, if you have a variable **a** with value **10**, and you assign it to a variable **b** (with **val b = a**), it is the value **10** that gets assigned. That means changes in **a** will not influence the value of **b**.

```kotlin
fun main() {
    var a = 10
    var b = a
    a = 20    
    //Changing a does not change b
    println(b) // 10
}
```

**Tip:** *You can use println or print to output content to the console.*

*Using println("test") will print data to a new line.  You can use it to display a value on the screen with a line break after it.*

*Using print("test")  will output your data (in this case the word 'test') but it will not place a blank line after it.*

### Understanding **val** and **var**

When you define variables, you must use one of two keywords:

- **val** is an abbreviation of 'value'. You use this modifier to specify variables that cannot be reassigned. In other words, code will not start if you try to assign a new value. As a consequence, they always represent the value that was assigned when the variables were created. That is why it makes sense to say that such variables represent a single value.
- **var** is an abbreviation of 'variable'. You use this modifier to specify variables that can be reassigned. So their value can change when the code runs, for example, being initially assigned a value of zero, then later being assigned a value of 1.

```kotlin
fun main() {
    // ERROR! val cannot be reassigned
    val value = "A"
    value = "B" 

    // OK! var can be assigned
    var variable = "A"
    variable = "B"
}
```

You might be wondering why **val** is ever used since **var** appears to be a more flexible way to assign a value.  The answer is readability, which means the ease with which a reader can understand the written code.

When you use **val**, it can be reassuring to know that the initial value stays the same. When you see **var**, you know it might change, so you need to be aware of how it changes. With **val**, it is enough to view its declaration to know what the value is.

That is why if you do not plan to change a variable value, it is preferable to use **val**. Using **val** and minimizing the number of unnecessary variable changes will increase the readability of your code.

### Variables and types

Each variable has a specific type. Variables of a certain type can only keep values of this type. For instance, an Int variable can store whole numbers but cannot store text.

By default, the type of the variable is the type of the value assigned to this variable during creation. Variable type cannot change once assigned. For instance, if you define a variable called **str** with an initial value of type **string**, like **ABC**, you can later assign **str** a different value of type **string**, but not of any other type.

```kotlin
fun main() {
    var str = "ABC" // The type of str is String
    str = "XYZ"
    str = 42 // ERROR! Int value cannot be assigned to a variable of type String
    str = true // ERROR! Boolean value cannot be assigned to a variable of type String
}
```

To specify the type, you use a colon and the name of the required type after the variable name.

```kotlin
fun main() {
    var str: String = "ABC"
    str = "XYZ"
}
```

There are a few reasons to use the explicit variable type. One is readability. Sometimes, the right side of the assignment might be complicated, and specifying a type to makes it easier to understand your code. Normally one might expect someone’s age to be stored as a numeric type. However, when the requirement is to combine the numeric with text, it’s better to specify the variable **age** explicitly as a string type.

```kotlin
fun main() {
    val age: String = "" + 42 + "!" 
}
```

Another reason that you might explicitly specify a type is when you need a value to include multiple subtypes. For instance, **any** is a data type that includes all other types. So **string**, **int** and **Boolean** are all subtypes of **any**. That means that if you define a variable called **userInputData** with a type of **any**, you can assign it any value you’ve learned about so far.

For example, if you define a variable **x** with type **any**, you can assign to it any value you’ve learned about so far.

```kotlin
fun main() {
    var x: Any = "ABC"
    println(x) // ABC
    x = 123
    println(x) // 123
    x = true
    println(x) // true
}
```

In this reading, you learned about the differences between variables and values and their associated keywords, **var** and **val**. You also learned about variable data types and how explicitly assigning a type to a variable can improve the readability of code.

### Numbers

in Kotlin, these are the four basic types representing numbers:

- **Int** is the default integer number representation when a whole number (such as 20) is specified.
- **Long** is an integer representation supporting larger numbers. You create it by using an **L** suffix.
- **Double** is the default decimal number representation. It holds values up to 15 or 16 decimal places.
- **Float** is an integer representation supporting smaller decimal numbers. It holds values up to 7 or 8 decimal places. You create it using the **F** or **f** suffix.

```kotlin
fun main() { 
    val a = 10 // the type of a is Int 
    val b = 2147483647L // the type of b is Long 
    val c = 10.0 // the type of c is Double 
    val d = 10F // the type of d is Float 
}
```

All numbers can be negative, and you can use underscores ('_') inside longer numbers to improve their readability.

```kotlin
fun main() { 
    val smallDebt = -0.72 
    println(smallDebt) // -0.72 
    val million = 1_000_000 
    println(million) // 1000000 
}
```

You can transform one number type into another using transformation functions. They start with the prefix **to** and then the type you want. For instance, to transform **Int** or **Long** into **Double**, use **toDouble()** as in the following example.

```kotlin
fun main() { 
    val i: Int = 10 
    val l: Long = i.toLong() 
    val d1: Double = i.toDouble() 
    val d2: Double = l.toDouble() 
    println(d1) // 10.0 
    println(d2) // 10.0 
}
```

With all numbers, you can do standard math operations like addition, subtraction, division or multiplication.

```kotlin
fun main() { 
    println(2 + 3) // 5 
    println(2 - 3) // -1 
    println(2 * 3) // 6 
    println(8 / 2) // 4 
 
    println(0.5 * 4.5) // 2.25 
    println(2.5 / 0.5) // 5.0 
}
```

There is also an operation called **remainder**, represented by the following symbol: **%**.  Remainder returns what would be left if you divide an integer by another integer.

```kotlin
fun main() { 
    println(10 % 3) // 1  
println(11 % 3) // 2 
    println(12 % 3) // 0 
    println(13 % 3) // 1 
     
   // The sign of the result is always the same as the sign of the left side 
    println(-1 % 3) // -1 
    println(1 % -3) // 1 
    println(-1 % -3) // -1 
}
```

When you carry out an operation between integer values, the result is an integer. If you conduct an operation between **Int** and **Long**, the result is **Long**. When you conduct operations between a decimal type and either an integer or a decimal type, the result is the decimal type. If you carry out an operation between **Float** and **Double**, the result is **Double**.

```kotlin
fun main() { 
    val a = 1 + 2L // the type of a is Long 
    val b = 1 + 2.0 // the type of b is Double 
    val c = 1.0F + 2 // the type of c is Float 
    val d = 1.0F + 2.0 // the type of c is Double 
}
```

But take care whenever you divide two integers because the result of this operation will be an integer. If the calculation results in a decimal, the decimal part of this operation is lost. To ensure fractions are retained, transform one of the values to a **Double** or **Float** before the math operation.

```kotlin
fun main() { 
    val a = 5 
    val b = 2 
    println(a / b) // 2 
    println(a.toDouble() / b) // 2.5 
}
```

### Precedence

Operational precedence is a math concept that refers to the sequence in which a calculation is evaluated. Operational precedence is respected in all Kotlin math operations. For example, 1 plus 2 times 3 is **7**, not **9**, because multiplication is always done before addition.

```kotlin
fun main() { 
    println(1 + 2 * 3) // gives a result of 7 
}
```

Where necessary, you can dictate the order of precedence by using parentheses.  In our amended example, the precedence is changed by putting the 1 + 2 part of the calculation into parentheses. This way, the addition is done before the multiplication, producing a result of **9**.

```kotlin
fun main() { 
        println((1 + 2) * 3) // gives a result of 9 
}
```

Remember that depending on the method used to calculate the desired value, the outcome can be very different. Consider a scenario where you are working on a small game project. You build some code to keep track of a player’s score and bonuses through the levels of the game.  Then you need to calculate their final score.   The formula you create is: **score1 + score2 * bonusScore = totalScore**

The correct way to score the game is to add score1 and score2 together and then multiply the result by the bonus score.   However, if you put that calculation into Kotlin, the multiplication is done first, then the addition, resulting in an incorrect player's final score.

To ensure the correct score is recorded you must override the built-in precedence by surrounding the calculation you want to perform first with parentheses.  Your amended  equation is: **(score1 + score2) * bonusScore**

These examples are basic, but they do indicate how careful you need to be when dealing with different values and different math operations. Always check that your math is calculated the way you intend. You can guarantee this by using parentheses to force the order of execution.

### Augmented assignments

Variables defined with **var** can have their value changed.

```kotlin
fun main() {
var a = 10
println(a) // 10
a = 20
println(a) // 20
}
```

This is often used to add or subtract something from the value.

```kotlin
fun main() { 
    var a = 10 
    println(a) // 10 
    a = a + 10 
    println(a) // 20 
    a = a + 10 
    println(a) // 30 
}
```

Since applying addition or subtraction to a value is a common operation, Kotlin has special support for that. Instead of **a = a + b** you can use **a += b**.

```kotlin
fun main() { 
    var a = 10 
    println(a) // 10 
    a += 10 
    println(a) // 20 
    a += 10 
    println(a) // 30 
}
```

This is called an augmented assignment, and it is supported for other operations as well, such as:

- **a += b** is an alternative to **a = a + b**,
- **a -= b** is an alternative to **a = a - b**,
- **a *= b** is an alternative to **a = a * b**,
- **a /= b** is an alternative to **a = a / b**,
- **a %= b** is an alternative to **a = a % b**.

```kotlin
fun main() { 
    var a = 10 
    println(a) // 10 
    a *= 3 
    println(a) // 30 
    a -= 12 
    println(a) // 18 
    a /= 3 
    println(a) // 6 
    a %= 4 
    println(a) // 2 
}
```

**Prefix and postfix operation**

In Kotlin, there are some different ways to add or subtract 1.

For example;

> **a = a+1**
>

or

> **a++**
>

and likewise for subtraction.

That **a++** is called a postfix operation, which means that if you use that operation in an arithmetic equation, the postfix operation isexecuted *after* the equation is evaluated.

For example:

> **var a = 5**
>

> **val eq = 6 + a++ // the result will be 11 and then a will be = 6**
>

> **valnewEq = 6+a // the result will be = 12**
>

A *prefix* operation works differently. If you use the prefix operation in an arithmetic equation, the prefix operation is executed *before* the equation is evaluated.

With the previous example a *prefix* operation works like this:

> **var a = 5**
>

> **val eq = 6 + ++ a// the result a will be 6 and then eq will be = 12**
>

> **valnewEq = 6+a // the result will be =12**
>

The same follows if you use postfix and prefix operations in subtraction (**a--** and **--a**) .

```kotlin
fun main() { 
    var a = 10 
    println(a) // 10 
    a++ 
    println(a) // 11 
    a-- 
    println(a) // 10 
}
```

### Char & String

Text is a very important part of everyday life, from books to newspapers, instant messages to advertisements. In the world of mobile applications, text is not only important for displaying buttons and labels but also for sending and receiving data. As such, there needs to be a way to represent text when programming.

In Kotlin, this is done using two basic types: **Char** and **String**, which you'll learn more about in this reading.

### **Char**

**Char** represents a single character. This can be a letter, a number, punctuation or another symbol. A **Char** value can be specified in single quotes. For example, to define a **Char** variable named **myChar** with the value set to the letter **a**, you would use the following code:

```kotlin
val myChar: Char = 'a'
```

### **String**

A **String** represents a sequence of characters, such as a word or sentence. A **String** value can be specified in double quotes. For example, to define a **String** variable named **myString** with the value set to the word **"Hello"**, you would use the following code:

```kotlin
val myString = "Hello”
```

If your text contains multiple lines, it is also possible to define this in a **String** variable in Kotlin by delimiting the text with triple quotes.

```kotlin
val myString = """Hello
This is a String. 
It is on multiple lines. 
"""
```

It is also possible to insert the value of variables into a **String** value. This is called a **String** template in Kotlin.

```kotlin
val age = 70 
val myString = "My age is $age"
```

A template expression starts with the **$** symbol. In the above example, the resulting **String** will be **“My age is 70”**.

### Converting a **Char** to a **String**

To convert a **Char** into a **String**, use the **toString()** function.

```kotlin
val myChar: Char = 'a'
val myString = myChar.toString()
```

### Appending to a **String**

To add additional text to the end of a **String**, use the **+** operator. It is important to note that this does not change the existing **String** variable but creates a completely new **String** variable.

```kotlin
val myString = "Hello"
//myString is still Hello after this operation.
val myLongStrong = myString + " World"
```

The following example shows how new variables are created when a **String** is modified.

```kotlin
fun main() {
    var s1 = "Hello"
    val s2 = s1 // s1 and s2 now point at the same string - "Hello"
    println(s1) // prints "Hello"
    println(s2) // prints "Hello"
    s1 += "world" // append "world" to s1
    println(s1) // prints "Hello world"
    println(s2) // still prints "Hello" because s2 still points to the String "Hello" while s1 is a new String object
}
```

### Checking the length of a **String**

It is possible to check how long a **String** is using the length property. For example, the length of the **String** value **Hello** will return **5**.

```kotlin
val myString = "Hello"
val myStringLength = myString.length
```

This means the **myStringLength** will have a value of **5**.

### Searching Strings

The **String** type has multiple functions for searching its contents. Below are examples.

**True if the String starts with Hel, otherwise false**

```kotlin
val myString = "Hello"
val startsWithHel = myString.startsWith("Hel")
```

**True if the String ends with lo, otherwise false**

```kotlin
val myString = "Hello"
val endsWithLo = myString.endsWith("lo")
```

**Get the first character**

```kotlin
val myString = "Hello"
val firstChar = myString.first()
```

**Get the last character**

```kotlin
val myString = "Hello"
val lastChar = myString.last()
```

**True if the String is equal to Hello, otherwise false**

```kotlin
val myString = "Hello"
val equalsHello = myString.equals("Hello")
```

There are many more search functions available in the **String** type. Information on these functions can be found in the Additional Resources at the end of this lesson.

## Manipulating Strings

The **String** type also has multiple functions for manipulating its contents.

```kotlin
val myString = "Hello"
val myUpperString = myString.uppercase()
```

**Convert the String to lowercase**

```kotlin
val myString = "Hello"
val myLowerString = myString.lowercase()
```

**Get all characters from the second character onwards**

Note: Counting starts at **zero. myString2** will have the value **ello**.

```kotlin
val myString = "Hello"
val myString2 = myString.substring(1)
```

It is important to note that Strings are immutable. This means that when you use a function that manipulates the **String**, it actually returns a new **String** instance.

### **Boolean**

Numbers and Strings have already been introduced in this course, and now the last basic operation type to learn about is a **Boolean**. A **Boolean** has two possible values, **true** and **false**, and can be used to tell users whether something is true or not. For instance, if you implement a website, you need to ask the user to accept the cookie policy. You then need to store information on whether the user accepted it or not, which can be represented by a variable. It is either **true** because the user accepted the policy or **false** because the user rejected the policy.

var cookiePolicyAccepted: Boolean = true

When you compare two values, the result is of type **Boolean**. You can check if two values are equal by using the double equal sign, and the result will always be a **Boolean**, so either **true** or **false**.  In Kotlin, you can use either the **== operator** or the **equals()** when comparing strings.

```kotlin
println("A" == "A") // true
println("A" == "B") // false
println(10 == 10) // true
println(20 == 10) // false
```

You can also check if two values are not equal to each other. For that, use an exclamation mark and an equal sign. You will notice that the results are exactly the opposite of what you had when you used the double equal sign.

```kotlin
println("A" == "A") // true 
println("A" == "B") // false 
println(10 == 10) // true 
println(20 == 10) // false 

println("A" != "A") // false 
println("A" != "B") // true 
println(10 != 10) // false 
println(20 != 10) // true
```

You can also compare values with less-than or greater-than signs. Here are a few examples of comparing numbers.

```kotlin
println(10 > 10) // false 
println(20 > 10) // true 
println(10 > 20) // false 

println(10 < 10) // false 
println(20 < 10) // false 
println(10 < 20) // true
```

As you can note, two identical values are not less-than or greater-than. If you want to check if a value is less-than or equal-to or greater-than or equal-to, there are special operators for that. You use the less-than or greater-than sign followed by the equal sign.

```kotlin
println(10 >= 10) // true 
println(20 >= 10) // true 
println(10 >= 20) // false 

println(10 <= 10) // true 
println(20 <= 10) // false 
println(10 <= 20) // true
```

You may have noticed that all of those comparisons produce either **true** or **false** results, which you call a Boolean type. You will find this useful in a subsequent lesson, for instance, when using the if-condition to execute some code only if a comparison returns **true**.  Keep reading to learn how to create these logical expressions.

### Logical Operations

Just like you can perform operations on numbers, you can also perform operations on **Boolean** values.  For example, think about the phrase, "if I run 5 miles and lift weights, I will buy pizza tonight". In order to buy pizza, both parts of the condition have to be met. The connection between the two conditions is called a logical operator.

Keep reading to learn how to construct these logical expressions in code.

### The 'and' operator (**&&**)

To help you understand logical operators, imagine a conversation between a young boy called Steven and his mother. He wants to play on the computer, so he asks his mother, and she says, "You can play on the computer, but only if you do your homework and clean your room." In programming, you can express this condition using an **and** operator (**&&**) between logical values

```kotlin
fun main() { 
    val finishedHomework = false // or true 
    val cleanedRoom = true // or false 
    val canPlayGames = finishedHomework && cleanedRoom 
    println(canPlayGames) 
}
```

Try editing this code in Kotlin Playgrounds and altering the **finishedHomework** and **cleanedRoom** values. Then run the code and note how it influences the result **canPlayGames** value. The **canPlayGames** is **true** only if both **finishedHomework** and **cleanedRoom** are **true**. In all the other cases, **canPlayGames** is **false**.

```kotlin
fun main() { 
    print(true && true)  // true 
    print(true && false)  // false 
    print(false && true)  // false 
    print(false && false)  // false 
}
```

Let's imagine another scenario involving Steven. Say Steven would like to get a puppy. This means that he needs time to look after the puppy because he will be responsible for it. In this scenario, Steven does have time, but he is not responsible enough to have a puppy, so the answer should be no.

```kotlin
fun main() { 
    val haveTime = True 
    val isResponsible = False 
    val canHavePuppy = isResponsible && haveTime 
    print(canHavePuppy) // false 
}
```

Let's take another example. Imagine that you need to verify a percentage value. A percentage has to be any value from 0 to 100 inclusive. You can use the following code to express this.

```kotlin
fun main() { 
    val percent = 47 
    val correct = percent >= 0 && percent <= 100 
    println(correct) // true 
}
```

### The 'or' operator (**||**)

Let's get back to Steven. He didn’t finish his homework, so he couldn't play on the computer. But then his friend calls and invites him to go to the cinema. When he asks his mother if he can go, she says, "You can go if you clean the car or cut the grass." This is how you could create such a condition in programming:

```kotlin
fun main() {
val carCleaned = false // or true
val grassCut = true // or false
val canGoToCinema = carCleaned || grassCut
println(canGoToCinema)
}
```

The operator **or** represents an alternative. It returns **true** if any of its sides returns **true**.

```kotlin
fun main() {
print(true || true)  // true
print(true || false)  // true
print(false || true)  // true
print(false || false)  // false
}
```

Let's examine some other examples using the or operator.

Let's say Steven can eat chocolate if he behaves well or cleans his room.

```kotlin
fun main() {
val behavedWell = false // or true
val cleanedRoom = false // or true
val canEatChocolate = behavedWell || cleanedRoom
println(canEatChocolate)
}
```

Another example is that the number of a percentage is incorrect if it is smaller than 0 or bigger than 100.

```kotlin
fun main() {
val percent = 47
val incorrect = percent < 0 || percent > 100
println(incorrect) // true
}
```

### The 'not' operator (**!**)

The last important logical operator is not (**!**), and it negates the Boolean value. So, it turns **true** into **false** and **false** into **true**.

```kotlin
fun main() { 
    println(!true) // false 
    println(!false) // true 

    val isAmazing = true 
    print(!isAmazing) // false 
    
    isBoring = false 
    print(!isBoring) // true 
}
```

A good analogy for the logical operator **not** is a minus before a number. It turns a negative number into a positive, and a positive into a negative.

```kotlin
fun main() { 
    val positive = 1 
    print(-positive) // -1 

    val negative = -1 
    print(-negative) // 1 
}
```

In programming, you can use negation multiple times.

```kotlin
fun main() {
println(!true) // false
println(!!true) // true
println(!!!true) // false
println(!!!!true) // true
println(!!!!!true) // false
}
```

The **not** operator is often a part of more complex logical expressions. For instance, when Steven's mom said, "You can play games if you pass the math exam and clean your room."

```kotlin
fun main() { 
    val failedMathExam = true 
    val roomCleaned = true 
    val canPlayGames = !failedMathExam && roomCleaned 
    println(canPlayGames) // false 
}
```

Notice that the negation here only negates the value of **failedMathExam**, not the result of the whole expression. It is because the **not** operator has higher precedence than **and** **or** operators. So **!true && false** returns **false**, because you first evaluate the negation and then **false && false**. It is similar to numbers. The expression **-10 + 20** gives **10** as a result, not **-30**. To change the precedence, you use parenthesis. So !**(true && false)** gives **true**, and **-(10 + 20)** gives **-30**.

```kotlin
fun main() { 
    println(!true && false) // false 
    println(!(true && false)) // true 
    println(-10 + 20) // 10 
    println(-(10 + 20)) // -30 
}
```

## Reading logical expressions

You may find much longer and more complex logical expressions. It helps to read them aloud. You can read it in the following way:

- **&&** as **and**,
- **||** as **or**,
- **!** in front of a value as **not** and in front of a bracket as **it is not true that**.

Now practice by reading the following logical expressions out loud:

- **cleanedRoom && passedTest** (should be **"cleaned room and passed test"**).
- **!isGrounded || passedTest** (should be **"is not grounded or passed test"**).
- **cleanedRoom && !passedTest** (should be **"cleaned room and not passed test"**).
- **!(isGrounded && !passedTest)** (should be **"it is not true, he is grounded and didn't pass the test"**)
- **!(!cleanedRoom || !passedTest)** (should be **"it is not true, he has not cleaned room or not passed test"**)

Some logical expressions can be simplified. There is a rule that **!(!a && !b)** can be replaced with **a || b** or **!(!a || !b)** can be replaced with **a && b**. That means that the expression **!(!cleanedRoom || !passedTest)** can be replaced with **cleanedRoom && passedTest** and the expression **!(isGrounded && !passedTest)** can be replaced with **!isGrounded || passedTest**.

### If&Else Conditional Statement

You use the **if** statement to invoke conditional code. In other words, the code will only run if a predicate is fulfilled. For example, Steven from the story used in an earlier reading can go to the cinema if he finishes his homework:

```kotlin
fun main() {
    val finishedHomework = true
    if (finishedHomework) {
        println("Can go to the cinema")
    }
}
```

The additional **else** block is used to provide an alternative for the cases when a predicate is not fulfilled.

```kotlin
fun main() {
    val finishedHomework = true
    if (finishedHomework) {
        println("Can go to the cinema")
    } else {
        println("Cannot go to the cinema")
    }
}
```

Often, the predicate is an expression that compares two values. For instance, if a value is smaller or bigger than another value.

```kotlin
fun main() {
    val i = 1 // or 5
    if (i < 3) {
        println("Smaller")
    } else {
        println("Bigger")
    }
    // Prints Smaller if i == 1, or Bigger if i == 5
}
```

### Using **if-else** as expressions

An **if-else** statement can be used as an expression. In other words, to return a value that can be stored in a variable. The returned value is the value returned by the body block that was chosen. In the code below, the predicate returns **true**, so the first body is chosen, so **10.0** is returned.

```kotlin
fun main() {
    val haveSomeExtraMoney = true
    val tip: Double =
        if (haveSomeExtraMoney) {
            10.0
        } else {
            0.0
        }
    println(tip) // 10.0
}
```

Inside **if-else** bodies, you can include more than one statement. The value returned by a body is the last expression it has.

```kotlin
fun main() {
    val haveSomeExtraMoney = true
    val tip: Double =
        if (haveSomeExtraMoney) {
            println("Here you go") // Here you go
            1.0 // this value is ignored, because it is not the last one
            5.0 // this value is ignored, because it is not the last one
            10.0
        } else {
            println("Sorry, I am broke")
            0.0
        }
    println(tip) // 10.0
}
```

However, if you have only one expression in your body, you can skip braces.

```kotlin
fun main() {
    val haveSomeExtraMoney = true
    val tip: Double = if (haveSomeExtraMoney) 10.0 else 0.0
    println(tip) // 10.0
}
```

### If-else-if

By placing one if-else block after another, you form a structure known as if-else-if. It is a structure that checks conditions one after another until it finds the first one that is fulfilled, and it calls its body. If all the conditions return false, the else block is called. This means that in the following code, if probability is smaller or equal to 40, then only Unlikely will be printed. If probability is over 40 but smaller or equal to 80, then only Likely will be printed. If probability is over 80 but smaller or equal to 100, then only Yes will be printed. Otherwise, What? will be printed.

```kotlin
fun main() {
    println("Is it going to rain?")
    val probability = 70
    if (probability <= 40) {
        println("Unlikely")
    } else if (probability <= 80) {
        println("Likely")
    } else if (probability < 100) {
        println("Yes")
    } else {
        println("What?")
    }
}
```

If-else-if is a popular structure in many languages but not in Kotlin. This is because there is a better alternative, called the when statement, but it's good to know how to use if-else-if in case you ever need it.

In this reading, you learned how to use the conditionals if, if-else, and if-else-if statements.

### When Conditional Statement

The **when** statement is an alternative to **if-else-if**. On every branch of the when statement, you can specify a predicate and a body. The body will be executed only for the first predicate that returns true. So it works just like **if-else-if,** but it's preferred because its syntax is better suited for multiple conditions. And thanks to the fact that it's a single statement, Kotlin can run this code faster than checking multiple **if-else-if** statements.

In the following code, if the **probability** is smaller or equal to 40, then only **Unlikely** will be printed. If the **probability** is over 40 but smaller or equal to 80, then only **Likely** will be printed. If **probability** is over 80 but smaller or equal to 100, then only **Yes** will be printed. Otherwise, **What?** will be printed. If you run the code, you should see **Likely** because the initial **probability** is 70, but feel free to change this value and run the code again.

```kotlin
fun main() {
println("Is it going to rain?")
val probability = 70
    when {
        probability < 40 -> {
        println("Unlikely")
        }
        probability <= 80 -> {
        println("Likely")
        }
        probability < 100 -> {
        println("Yes")
        }
        else -> {
            println("What?")
        }
    }
}
```

Just like in an **if** statement, braces are needed only for bodies with more than one statement. If there is only one statement in a body, you can leave out the braces.

```kotlin
fun main() {
println("Is it going to rain?")
val probability = 70
    when {
        probability < 40 -> println("Unlikely")
        probability <= 80 -> println("Likely")
        probability < 100 -> println("Yes")
        else -> println("What?")
    }
}
```

The **when** statement can also be used as an expression in order to produce a value. The only rule is that a **when** statement must have an **else** block so that it has a value to return in case no other block is chosen.

In the following code, the **text** value depends on which branch is chosen by the when expression.

```kotlin
fun main() {
println("Is it going to rain?")
val probability = 70
val text = when {
        probability < 40 -> "Unlikely"
        probability <= 80 -> "Likely"
        probability < 100 -> "Yes"
        else -> "What?"
    }
    println(text)
}
```

There is also another form of the **when** statement. If you add a value in brackets after the **when** keyword, then in each branch, Kotlin compares this value to other values. In the following example, when **number** is 1, the **when** statement chooses the branch with a value of 1 and prints, **Missed hit**. When **number** is 2, 3, 4 or 5, the second branch is chosen, and **Hit with value {number value}** is printed. When the value is 6, the last branch is chosen, and **Critical hit** is printed.

```kotlin
fun main() {
val number = 1 // or 2, 3, 4, 5, 6
    when (number) {
        1 -> {
            println("Missed hit")
        }
        2, 3, 4, 5 -> {
            println("Hit with value $number")
        }
        6 -> {
            println("Critical hit")
        }
    }
}
```

Such a **when** statement can be used as an expression as well. In this example, it is used to produce a text value. Notice that you needed to add an **else** block for the case when the value of the **number** variable is not one of the values handled in the other when branches. So if the number is 10, then **Unsupported value** will be printed.

```kotlin
fun main() {
val number = 1 // or 2, 3, 4, 5, 6
val text = when (number) {
        1 -> "Missed hit"
        2, 3, 4, 5 -> "Hit with value $number"
        6 -> "Critical hit"
        else -> "Unsupported value"
    }
    println(text)
}
```

The when expression can be simplified, thanks to the feature known as a range check. In some branches, the condition might be checking if a value is inside a collection or a range. In the following example, instead of 2, 3, 4, , 2..5 was used, so instead of providing values to compare to, it checks if the value is in a range of values from 2 to 5. The syntax is as follows: start with the in keyword, and then specify either a collection or a range that might contain the value or not. Both collections and ranges will be covered later in this course.

```kotlin
fun main() {
val number = 1 // or 2, 3, 4, 5, 6
val text = when (number) {
        1 -> "Missed hit"
        in 2..5 -> "Hit with value $number"
        6 -> "Critical hit"
        else -> "Unsupported value"
    }
    println(text)
}
```

### Type check

was explained earlier in the course, every value has a certain type. For instance, 123 is of type **Int**, and **"ABC"** is of type **string**. When you have a value, you can check if it is of a certain type using the **is** keyword. Here are a few examples:

```kotlin
fun main() {
    var value = "ABC"

    println(value is String) // true
    println(value is Int) // false
    println(value is Boolean) // false
    println(value is Any) // true

    value = 123

    println(value is String) // false
    println(value is Int) // true
    println(value is Boolean) // false
    println(value is Any) // true
}
```

Type-check can also be used as a branch in a when statement with a value. This is a popular pattern in Kotlin to decide what action should be performed based on a variable type.

```kotlin
fun main() {
val something: Any = "ABC" // or 123, 0.1, true
    when (something) {
        is String -> println("This is String")
        is Int -> println("This is Int")
        is Double -> println("This is Double")
        is Boolean -> println("This is Boolean")
    }
    println(something)
}
```

### While Statement

Code is executed line by line, from the beginning to the end. So if you start the code inside **main**, the first line calls **print(1)**, and at the second one **print(2)**, the result is 12.

```kotlin
fun main() {
    print(1)
    print(2)
}
```

The order in which lines are executed is called control flow. The default order is statement by statement (line by line), from top to bottom. However, it is important to note that some structures can change this order. The **if** condition jumps over a specific block of code (its body) when its condition is not satisfied (returns **false**).

```kotlin
fun main() {
    println("Will be printed")
    if (true) {
        print("Will be printed")
    }
    if (false) {
        print("Will not be printed!")
    }
        println("Will be printed")
}
```

Until now, a line of code could not be called more than once during single program execution. That is a big limitation that you can work around with loops that allow executing a block of code multiple times.

The first loop you will learn about is the **while** loop. To a certain degree, it is similar to an **if** condition. Its structure is the same, except for using the **while** keyword instead of **if**. In both cases, if the predicate returns **false**, the body is never executed.

```kotlin
fun main() {
    while (false) {
        println("Will not be printed")
    }
    if (false) {
        println("Will not be printed")
    }
}
```

The difference becomes clear when the predicate returns **true**. In both cases, the body is executed. After that the **if** condition ends, but the **while** condition checks the predicate again. The **while** statement will print the body for as long as its condition returns **true**. That means you should not use **while** conditions with a predicate that will always return **true**. Such a code will run forever unless you stop it.

```kotlin
fun main() {
    while (true) {
        println("Prints forever!")
    }
}
```

Let's examine a few examples of how you might use the **while** loop. Starting with a code that prints its body just once.

```kotlin
fun main() {
    var toBePrinted = true
    while (toBePrinted) {
        println("Will be printed once")
        toBePrinted = false
    }
}
```

Here is a code that calls its body for numbers from 0 to 2.

```kotlin
fun main() {
    var printedTimes = 0
    while (printedTimes <= 2) {
        println("Line $printedTimes");
        printedTimes += 1
        // or
        // printedTimes = printedTimes + 1
    }
}
```

```kotlin
Line 0
Line 1
Line 2
```

### Mathematical sequences

Let's use the **while** loop to print some mathematical sequences. Let's have the first sequence start at 0, go up by 7 each step, and stop before it gets larger than 100. You could implement this by declaring a variable with an initial value of 0, then writing a **while** loop. The loop should only work when the current number is smaller than 100. Inside the body, you will print the current number and then add 7 to its value. That is all you need to display in the described sequence.

```kotlin
fun main() {
    var num = 0
    while (num < 100) {
        println(num)
        num += 7 // or num = num + 7
    }
}
```

The next sequence will start at the number 1, and each next number will be two times bigger. You will also stop when your number is bigger than 100. So you can start with a variable with an initial value of 1, write a **while** loop with a condition that the number is smaller than 100, and double the current number inside the **while** loop's body.

```kotlin
fun main() {
    var num = 1
    while (num <= 100) {
        println(num)
        num *= 2 // or num = num * 2
    }
}
```

In the last example, you will make a sequence of the squares of all the whole numbers and stop the sequence before the squared value is greater than 100. For that, you will use a **while** loop to iterate over the whole numbers, and you will print the square of each of them. The predicate will stop the loop when the square is larger than 100.

```kotlin
fun main() {
    var i = 1
    while (i * i <= 100) {
        println(i * i)
        i++
        // or i += 1
        // or i = i + 1
    }
}
```

### For Loop

To call code for each number from **a** to **b**, including **b**, use the range **a..b** inside a **for-loop**. The following code block should print the numbers **0, 1, 2, 3, 4 and 5**.

```kotlin
fun main() {
    val a = 0
    val b = 5
    for (i in a..b) {
        println(i)
    }
}
```

To call code for each number from **a** to **b**, excluding **b**, use a range **a until b** inside a **for-loop**. The following code block should print the numbers **0, 1, 2, 3 and 4**.

```kotlin
fun main() {
    val a = 0
    val b = 5
    for (i in a until b) {
        println(i)
    }
}
```

To call code for each number from **a** to **b**, where **a** is bigger than **b**, and the step should be **-1**, use **a downTo b** inside a **for-loop**. The below code should print the numbers **5, 4, 3, 2, 1 and 0**.

```kotlin
fun main() {
    val a = 5
    val b = 0
    for (i in a downTo b) {
        println(i)
    }
}
```

To call code for each number from **a** to **b**, with a step **c**, use **a..b step c** inside a **for-loop**. The code below should print the numbers **0, 3, 6 and 9**.

```kotlin
fun main() {
    val a = 0
    val b = 10
    val c = 3
    for (i in a..b step c) {
        println(i)
    }
}
```

To call code for each number from **a** to **b**, excluding **b**, with a step **c**, use **a until b step c** inside a **for-loop**. The below code should print the numbers **0, 3 and 6**.

```kotlin
fun main() {
    val a = 0
    val b = 9
    val c = 3
    for (i in a until b step c) {
        println(i)
    }
}
```

To call code for each number from **a** to **b**, where **a** is bigger than **b**, with a step **-c**, use **a downTo b step c** inside a **for-loop**. The below code should print the numbers **10, 7, 4 and 1**.

**Note**: in kotlin, The **step** accepts only positive numbers even in case using **downTo** .

```kotlin
fun main() {
    val a = 10
    val b = 1
    val c = 3
    for (i in a downTo b step c) {
        println(i)
    }
}
```

You can use this to generate the text for a silly song. Start the code below to find out what it's going to print.

```kotlin
fun main() {
    for (num in 5 downTo 1) {
        println("$num lemonades are left")
        println("Glupglupglup")
    }
    println("That is it")
    println("Now I have to go")
}
```

### Nested Loop

In an earlier video, you learned how to display a triangle made up of stars using a nested **for-loop**. You've explored how to make a triangle that starts with one star and ends with five like the one below.

```kotlin
*
**
***
****
*****
```

```kotlin
fun main() {
    for (i in 1..5) {
        for (j in 1..i) {
            print("*")
        }
        println()
    }
}
```

### Parametrizing a triangle

Notice that you can easily parametrize it. If you want to have this triangle but a size 10, you can achieve that by changing only one value.

```kotlin
fun main() {
    val height = 10
    for (i in 1..height) {
        for (j in 1..i) {
            print("*")
        }
        println()
    }
}
```

You'll end up with a triangle like this one:

```kotlin
*
**
***
****
*****
******
*******
********
*********
**********
```

### **downTo** function

You've also learned how to make a triangle that starts with five stars and ends with one.

```kotlin
*****
****
***
**
*
```

```kotlin
fun main() {
    for (i in 1..5) {
        val numberOfStars = 6 - i
        for (j in 1..numberOfStars) {
            print("*")
        }
        println()
    }
}
```

There is also an alternative way to implement that. You can use the **downTo** function, and in such a case, the **for-loop** variable does not indicate what the row number is. Instead, it indicates how many stars you should have in the following row.

```kotlin
fun main() {
    for (numberOfStars in 5 downTo 1) {
        for (i in 1..numberOfStars) {
            print("*")
        }
        println()
    }
}
```

It can also be easily parametrized to a certain height:

```kotlin
fun main() {
    val height = 10
    for (numberOfStars in height downTo 1) {
        for (j in 1..numberOfStars) {
            print("*")
        }
        println()
    }
}
```

You'll have a triangle like this one:

```kotlin
**********
*********
********
*******
******
*****
****
***
**
*
```

### Other shapes with stars

Let's explore some other shapes that you might form with stars. Let's start with the following:

```kotlin
*
***
*****
***
*
```

### How do you produce it?

The answer is to first make one triangle and then another one. Notice that in this triangle, you add two stars at each step until the desired width is reached. Let's assume that you will parametrize your triangle by its maximal width. Then you will use one **for-loop** printing upper stars. So it should start at 1 star, make step 2, and add **until width**. The second **for-loop** will start at **width**, go down to 1, with a step 2. Notice that in the first **for-loop**, you should use **until** instead of **..**, because if you don't, then the **width** number of stars will be printed twice: both by the first and by the second for-loop.

```kotlin
fun main() {
    val width = 5
    for (i in 1 until width step 2) {
        for (j in 1..i) {
            print("*")
        }
        println()
    }
    for (i in width downTo 1 step 2) {
        for (j in 1..i) {
            print("*")
        }
        println()
    }
}
```

Now, let's use a **for-loop** to print the following triangle:

```kotlin
 		*
   **
  ***
 ****
*****

```

This one is more complicated because, for each line, you first need to print a certain number of spaces and then a number of stars. So let's use a **for-loop**, where the **i** variable is the number of rows. In the first row, you need 4 spaces and 1 star. In the second row, you need 3 spaces and 2 stars. In the third row, you need 2 spaces and 3 stars. Did you notice the pattern? The number of spaces should be **5 - i**, and the number of stars should be **i**.,

```kotlin
fun main() {
    for (i in 1..5) {
        val numberOfSpaces = 5 - i
        for (j in 1..numberOfSpaces) {
            print(" ")
        }
        val numberOfStars = i
        for (j in 1..numberOfStars) {
            print("*")
        }
        println()
    }
}
```

Let's try something different and print an isosceles triangle that should look as follows:

```kotlin
    *
   ***
  *****
 *******
*********
```