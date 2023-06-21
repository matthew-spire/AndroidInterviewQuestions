- **Null Safety in Kotlin**
  - Kotlin's type system aims to eradicate null references from the code.
  - Kotlin provides Safe Call (?.), Elvis (?:) and Not Null Assertion (!!) operators to handle null encounters.
<br></br>

- **Safe Call, Elvis and Not Null Assertion Operators in Kotlin**
  - Safe Call operator (?.): Performs an action only when a specified reference holds a non-null value.
  - Elvis Operator (?:): Returns a non-null value or a default value when the original variable is null.
  - Not Null Assertion Operator (!!): Changes a null value to a non-null type and throws an exception if the value is null.
<br></br>

- **What does Kotlin support that Java does not?**
  - Null Safety
  - Coroutines Support
  - Data Classes
  - Functional Programming
  - Extension Functions
  - Data Type Inference
  - Smart Casting
  - No Checked Exceptions
<br></br>

- **Function Extension in Kotlin**: Allows users to define a method outside of the main class, providing a way to add or remove method functionality without altering the class itself.
<br></br>

- **Companion Object in Kotlin**
  - Declared inside a class and marked with the `companion` keyword
  - Used to create members (functions and variables) that can be accessed inside the class without having an instance of the class, much like `static` members in Java
  - Common usage: When you need a factory method that can return an instance of the class
<br></br>

- **Difference Between "open" and "public" Keywords in Kotlin**
  - The "open" keyword in Kotlin means "open for expansion" i.e., allows other classes to inherit from it, unlike "final" in Java.
  - If no visibility modifier is specified, the "public" is used by default, meaning the declarations will be accessible everywhere inside the program.
<br></br>

- **Mutable List vs Immutable List in Kotlin**
  - A mutable list is used if the collection will change as part of the design, while an immutable list is used if the model is only meant to be viewed.
  - Immutable lists are preferred as they promote functional programming and are easier to understand and debug.
<br></br>

- **Lateinit in Kotlin**
  - The "lateinit" keyword is used for late initialization of a variable.
  - This is useful in scenarios like variable initialization in lifecycle methods in Android, using Dagger for DI, setup for unit tests, and annotations in Spring Boot.
<br></br>

- **Lazy Initialization in Kotlin**
  - Lazy initialization is used to delay the initialization of an object until it's used for the first time, making the code more efficient and faster.
  - It's used in cases where object initialization is time-consuming, causing the entire class creation process to be delayed.
<br></br>

- **Difference between "lateinit" and "lazy" initialization**

|                     | `lateinit`                    | `lazy`                         |
|---------------------|-------------------------------|--------------------------------|
| **Initialization**  | Deferred until assignment     | Deferred until first access    |
| **Keyword**         | `lateinit`                    | `by lazy`                      |
| **Mutability**      | Mutable (`var`)               | Read-only (`val`)              |
| **Nullability**     | Non-null                      | Non-null                       |
| **Thread Safety**   | Not guaranteed                | Guaranteed (by default)        |
| **Use Cases**       | Mostly for Android Views & DI | Expensive computations & caching |
<br></br>

- **Coroutines in Kotlin**
    - Not part of Kotlin's standard library; instead, the kotlinx.coroutines library is used.
    - High-level coroutine-enabled primitives like launch and async.
    - Lightweight as they don't allocate new threads when created but use predefined thread pools and intelligent scheduling.
    - Can be paused and resumed in the middle of their execution.
<br></br>

- **Scope Functions in Kotlin**
    - Functions that execute a block of code within the context of an object, creating a temporary scope.
    - Types of scope functions include:
        - **let**: Frequently used for null safety calls.
        - **apply**: Used to operate on receiver object members, primarily to initialize them.
        - **with**: Recommended when calling functions on context objects without supplying the lambda result.
        - **run**: A combination of 'let' and 'with' functions. Used when the object lambda involves both initialization and computation of the return value.
        - **also**: Used for additional operations after the object members have been initialized.
<br></br>

- **Suspend Functions in Kotlin**
    - Functions that can be started, paused, and resumed.
    - Can only be invoked from another suspend function or from a coroutine.
    - Can suspend coroutine execution without blocking the current thread.
<br></br>

- **Sealed Classes in Kotlin**
    - Used for constrained or bounded class hierarchies.
    - Constructors are by default private and cannot be instantiated.
    - Provide type safety by limiting the types that can be matched at compile time.
<br></br>

- **Backing Field in Kotlin**
    - An auto-generated field for any property that may only be used inside accessors.
    - Used to avoid recursive call of an accessor, which would result in a StackOverflowError.
<br></br>

- **Difference between launch/join and async/await in Kotlin**
    - **launch/join**: launch is used to start and stop a coroutine. join is used to wait for the launched coroutine to complete.
    - **async/await**: async initiates a coroutine that computes a result. await is used on the result, represented by an instance of Deferred.
<br></br>
