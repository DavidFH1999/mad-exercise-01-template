# MAD - Exercise 01
## Tasks
* Watch the Kotlin Crashcourse Video in Moodle or complete the tutorials **[Introduction to programming in Kotlin](https://developer.android.com/courses/pathways/android-basics-compose-unit-1-pathway-1)** and **[Kotlin fundamentals](https://developer.android.com/courses/pathways/android-basics-compose-unit-2-pathway-1
)**.
* Answer the questions inside this Readme.md file and push it to your repository.
* Submit your coding solution of the Number Guessing Game inside the repository.
* Submit the link to your repository in Moodle.

## Questions
### Describe how Kotlin handles null safety. What are nullable types and non-null types in Kotlin? (0,5 points)

<span style="color:blue">Provide your answer here! </span>
>These code snippets shows Kotlin's null safety mechanisms, including the use of non-null and nullable types, and how to safely access and manipulate nullable types using the safe call operator, Elvis operator, non-null assertion operator, and safe casts.

```kotlin
// 1. Non-null Types
var nonNullableString: String = "I'm non-nullable!" // Non-null type, cannot hold null
// nonNullableString = null // Uncommenting this line would cause a compile-time error

// 2. Nullable Types
var nullableString: String? = null // Nullable type, can hold null
// Working safely with nullable types:

// Safe Call Operator (?.)
// Use the safe call operator to safely access properties or methods on nullable types.
val lengthSafeCall = nullableString?.length // Will be null if nullableString is null

// Elvis Operator (?:)
// Use the Elvis operator to provide a default value if the expression on the left is null.
val lengthElvis = nullableString?.length ?: 0 // Will be 0 if nullableString is null

// Non-null Assertion Operator (!!)
// Forces a nullable type to be treated as non-null, throws NullPointerException if it's null.
val lengthNonNullAssert = nullableString!!.length // Will throw NullPointerException if nullableString is null

// Safe Casts (as?)
// Attempts to cast a value to the specified type, returns null instead of throwing an exception if the cast isn't possible.
val nullableInt: Int? = nullableString as? Int // Will be null because the cast is not possible

```

### What are lambda expressions and higher order functions in Kotlin? Why would you store a function inside a variable? (0,5 points)

<span style="color:blue">Provide your answer here!</span>
> Lambda expressions are essentially unnamed functions that are defined and passed around as values.
```kotlin
// Define a lambda expression that takes two Ints and returns their sum.
val sumLambda: (Int, Int) -> Int = { a, b -> a + b }

// Use the lambda expression.
val result = sumLambda(5, 3) // result is 8
// This calls the lambda, passing in 5 and 3 as arguments.
```
> Higher-order functions can take functions as parameters or return them.
```kotlin
// Define a higher-order function that takes an operation as a parameter and applies it.
fun performOperation(x: Int, y: Int, operation: (Int, Int) -> Int): Int {
    return operation(x, y)
}

// Call the higher-order function with a lambda expression.
val multiplicationResult = performOperation(4, 2, { a, b -> a * b })
// operation is a lambda that multiplies the two numbers.
```

> Functions in Kotlin can be stored in variables, allowing you to pass around behavior and change it dynamically.
```kotlin
// Store a lambda expression in a variable.
var myComparator: (Int, Int) -> Boolean = { a, b -> a > b }

// Use the function stored in the variable.
println(myComparator(5, 4)) // Prints: true

// Change the lambda expression stored in the variable.
myComparator = { a, b -> a < b }

// Use the new function stored in the variable.
println(myComparator(5, 4)) // Prints: false
```

### Provide a solution for the following number guessing game inside `App.kt`. (3 points)

## Number Guessing Game in Kotlin
The game is a simple number guessing game. The task is to generate a random, max 9-digit, number. The number must **not contain repeating digits**. Valid digits are 1-9.
Ask the user to guess the max 9-digit number. The game is finished when the user guesses the correct digits in the correct order.
In each round, the user gets feedback about the number of correct digits and the number of correct digits in the correct position.
The output should be in the format "n:m", where "n" is the number of digits guessed correctly regardless of their position, 
and "m" is the number of digits guessed correctly at their correct position. Here are some examples:

This example shows the game flow with 4-digits to guess (the default argument)

Generated number: 8576
-	User input: 1234, Output: 0:0
-	User input: 5678, Output: 4:1
-	User input: 5555, Output: 1:1
-	User input: 3586, Output: 3:2
-	User input: 8576, Output: 4:4 -> user wins

Take a look into the provided code structure in `src/main/kotlin/App.kt`. Implement the following methods (lambda expressions):
- _playNumberGame(digitsToGuess: Int = 4)_ (1 point): The main game loop that handles user input and game state. Make use of _generateRandomNonRepeatingNumber_ and _checkUserInputAgainstGeneratedNumber_ here. This function also utilizes a default argument 
- _generateRandomNonRepeatingNumber_ (1 point): A lambda expression that generates a random number with non-repeating digits of a specified length.
- _checkUserInputAgainstGeneratedNumber_ (1 point): A lambda expression that compares the user's input against the generated number and provides feedback.

``CompareResult.kt`` This class is a data structure which helps with bundling the result of the comparison of the user input and the generated number. Look at the toSting() and use it in your output.

Run the project with `./gradlew run` and test your implementation with the provided tests in `src/test/kotlin/AppTest.kt` with `./gradlew test`.

# Project Structure
The project is structured into two main Kotlin files:

**App.kt**: Contains the main game logic and functions.

**AppTest.kt**: Contains unit tests for the various functions in App.kt.

