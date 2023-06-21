- **Null Safety in Kotlin**
  - Kotlin's type system aims to eradicate null references from the code.
  - Kotlin provides Safe Call (?.), Elvis (?:) and Not Null Assertion (!!) operators to handle null encounters.
<br></br>

- **Safe Call, Elvis and Not Null Assertion Operators in Kotlin**
  - Safe Call operator (?.): Performs an action only when a specified reference holds a non-null value.
  - Elvis Operator (?:): Returns a non-null value or a default value when the original variable is null.
  - Not Null Assertion Operator (!!): Changes a null value to a non-null type and throws an exception if the value is null.
<br></br>

- **Differences Between Kotlin and Java**
  - Null Safety: Kotlin has non-nullable variables by default, providing safety against null pointer exceptions which are a common problem in Java.
  - Coroutines Support: Kotlin has support for coroutines, allowing more efficient execution of long-running tasks compared to Java.
  - Data Classes: Kotlin supports data classes which can be declared simply with the keyword "data", providing automatic generation of constructors, getters, setters, and other methods.
  - Functional Programming: Kotlin supports both procedural and functional programming and has several useful features such as lambda expressions and higher-order functions.
  - Extension Functions: Kotlin allows the addition of new functionality to an existing class with extension functions, a feature not present in Java.
  - Data Type Inference: Kotlin provides data type inference, meaning we don't have to declare the type of each variable based on the assignment it will handle.
  - Smart Casting: Kotlin provides smart casting with the keyword "is-checks", simplifying casting operations.
  - Checked Exceptions: Kotlin does not have checked exceptions, making exception handling different compared to Java.
<br></br>

- **Function Extension in Kotlin**: Allows users to define a method outside of the main class, providing a way to add or remove method functionality without altering the class itself.
<br></br>

- **Companion Object in Kotlin**
  - Kotlin does not have a "static" keyword like Java for declaring class members.
  - Instead, Kotlin uses "companion objects" to achieve the same functionality.
  - Companion objects are declared using the "companion" keyword in front of the object definition.
  - All the required static member functions and member variables can be kept inside the companion object.
<br></br>

- **Difference Between "open" and "public" Keywords in Kotlin**
  - The "open" keyword in Kotlin means "open for expansion" i.e., allows other classes to inherit from it, unlike "final" in Java.
  - If no visibility modifier is specified, the "public" is used by default, meaning the declarations will be accessible everywhere inside the program.
<br></br>

- **Advantages of Kotlin over Java**
  - Data class: In Kotlin, data classes handle hashCode, toString, and equals methods automatically unlike Java.
  - Getter and setter patterns: No need to rewrite the getter and setter methods for each variable in Kotlin.
  - Extension Functions: Kotlin provides support for extension functions, which Java does not.
  - Support for one common codebase with the Kotlin Multi-Platform framework.
  - Built-in null safety support.
  - Less prone to errors: Kotlin is more concise and expressive than Java.
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
  - "lateinit" is used to delay the initialization to a later point, while "lazy" initialization is used to initialize an object only when it is used.
  - "lateinit" can initialize the object from anywhere in the program, but "lazy" initialization can only be initialized using the initializer lambda.
  - In "lateinit", multiple initializations are possible, while in "lazy" initialization, only a single initialization is possible.
  - "lateinit" is not thread-safe, but "lazy" initialization is thread-safe by default.
  - "lateinit" only works with "var", while "lazy" initialization only works with "val".
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
