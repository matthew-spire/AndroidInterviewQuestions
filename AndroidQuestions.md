# Android Interview Questions

# Core

## AndroidManifest.xml

Q: What is `AndroidManifest.xml`?

A: The `AndroidManifest.xml`:

- Summary
  - Crucial configuration file in an Android app that provides information about the app's components, permissions, features, metadata, and more
  - Helps the Android system, build tools, and the Google Play Store manage and interact with the app

- Is a fundamental and essential configuration file in an Android application
- Serves as a central source of information about the app for the Android OS, the app build tools, and the Google Play Store
- Is located at the root of the application's project directory, under the `/app/src/main` folder

- Key roles and purposes of the `AndroidManifest.xml` are:
  - Declare all the app components (Activities, Services, Broadcast Receivers, and Content Providers) used by the application &rarr; Allows the Android system to recognize and manage these components
  - Defining app permissions
    - Used to request permissions required by your app to access sensitive or protected resources, such as camera, location, or internet access
    - Permissions are presented to the user during installation or runtime, depending on the Android version
  - Specifying hardware and software features
    - Declare the hardware and software features the app requires or utilizes
    - Used by the Google Play Store to filter apps for users based on their devices' capabilities
  - Setting app metadata
    - Metadata about the app, such as the app's package name, version code, and version name
    - Used by the Android system and the Google Play Store to manage app updates and compatability
  - Intent Filters
    - Define how the app's components can be activated by the Android system or other apps
    - Help specify the actions, data types, and categories the (app's) components can handle
  - App theme and icon
    - Used to set the application-wide theme and app icon, which are used by the launcher and other parts of the system

## Android Application Components

Q: What are the Android application components?

A: The Android application components include:

- Activities
  - Represents a single screen with a UI
  - Responsible for managing user interactions and rendering UI elements
  - Has a lifecycle that is managed by the Android OS
  - Can be started by other components via Intents and can return results to the caller

- Services
  - Is a component that runs in the background to perform long-running tasks or tasks that do not require a UI
  - Can run even when the app's Activities are not visible on the screen
  - Has two main types:
    - Started Services &rarr; Triggered by an explicit start command and run until they complete their tasks or are explicitly stopped
    - Bound Services &rarr; Bound to other components (e.g., an Activity) and run as long as the binding exists

- Broadcast Receivers
  - Are components that respond to system-wide or app-specific broadcast messages called Intents
  - Act as a gateway for the app to react to events such as system boot completed, connectivity changes, or a custom event sent by another app
  - Are typically short-lived, and their main purpose is to create notifications, start Services, or schedule tasks

- Content Providers
  - Are components that manage and share app data with other apps or components
  - Act as a common data storage layer, allowing data to be securely shared between different apps or components using a standardized interface
  - Use URIs to uniquely identify data sets and support CRUD operations through the ContentResolver object

## Context

Q: What is `Context`? How is `Context` used?

A: In Android development, `Context`:

- Is a fundamental concept that represents the current state of the application or an interface to the system

- Provides access to resources, system services, and other app-specific information

- Is essentially a connection between your app and the Android operating system

- Has different types, each with its specific use case, including:

  - Application Context
  - Activity Context
  - Service Context

- Can be used for the following:
  - Accessing resources (e.g., colors, dimensions, strings, etc.) in the `res` folder
  - Launching activities &rarr; Context is needed to create an intent and then call `startActivity()` method
  - Accessing system services (e.g., LocationManager, NotificationManager, etc.) &rarr; Obtained by calling `getSystemService()` method and passing in the appropriate constant
  - Accessing app-specific data (e.g., shared preferences and databases)
  - Inflating layouts &rarr; LayoutInflater requires a Context to work
  - Interacting with other (app) components like Services, BroadcastReceivers, and ContentProviders

- Needs to be used correctly, otherwise memory leaks or unexpected behavior might occur

## Application Class

Q: What is `Application` class?

A: The `Application` class in Android is:

- The base class within an Android app that contains all other components such as Activities and Services
- The `Application` class, or any subclass, is instantiated before any other class when the process for the app/package is created

# Activity, Fragment, and Lifecycle

## Activity and Fragment

Q: What is the difference between an Activity and a Fragment? Explain the relationship between the two.

A: Activity and Fragment are essential components used for creating user interfaces, but they serve different purposes and have distinct characteristics.

- Activity
  - Represents a single screen or window in the application that the user can interact with
  - Acts as a container for the UI components and is responsible for managing their lifecycle
  - Has its own lifecycle (onCreate, onStart, onResume, onPause, onStop, onDestroy) managed by the Android OS
  - Can be invoked by other components, such as Services or BroadcastReceivers, via Intents
  - Can be added to the back stack, allowing users to navigate back to the previous screen using the back button
<br></br>
- Fragment
  - Is a modular and reusable part of the UI that can be inserted into an Activity
  - Is not a standalone component and must always be associated with an Activity
  - Has its own lifecycle (onAttach, onCreate, onCreateView, onStart, onResume, onPause, onDestroyView, onDestroy, onDetach) that is influenced by the hosting Activity's lifecycle
  - Enable the creation of responsive and flexible UI designs by allowing developers to combine multiple Fragments within a single Activity
  - Can be added to the back stack independently of the Activity, allowing users to navigate back through Fragment transactions
<br></br>
- Relationship between Activity and Fragment
  - An Activity can host one or more Fragments, and a Fragment is always part of an Activity
  - Fragments can be dynamically added, replaced, or removed from an Activity during runtime using Fragment transactions through the FragmentManager
  - The lifecycle of a Fragment is closely tied to the lifecycle of its hosting Activity
    - E.g., when an Activity is paused, all Fragments within the Activity are also paused
  - Communication between an Activity and its Fragments is typically done using interfaces, allowing the Activity to respond to events in the Fragment and vice versa
<br></br>
- Summary
  - Activities are standalone UI components representing a single screen
  - Fragments are modular, reusable UI components that can be hosted within an Activity
  - Fragments are used to create flexible and responsive UI designs by combining multiple UI components within a single Activity
  - The lifecycle of a Fragment is closely tied to the hosting Activity, and communication between the two is typically achieved using interfaces

## Fragment Over Activity

Q: When should you use a Fragment rather than an Activity?

A:

- When the app has UI components that will be used across multiple screens
- When multiple views can be displayed side-by-side just like ViewPager

## Communicating Between Activities

Q: How would you communicate between two Activities?

A:

- You can communicate between Activities by sending data using Intents
  - An Intent is a messaging object that you can use to request an action from another Activity
  - Pass data in the form of key-value pairs known as extras

- Process
  - Create a new Intent in the sender Activity and add data as extras
  - In the receiver Activity, retrieve the extras from the Intent

- Send data back from the receiver Activity to the sender Activity
  - Use `startActivityForResult()` and `onActivityResult()`
  - Start the receiver Activity using `startActivityForResult()` in the sender Activity
  - In the receiver Activity, set the result and data before finishing the Activity
  - Override `onActivityResult()` in the sender Activity to retrieve the result

## Communicating Between Fragments

Q: How would you communicate between two Fragments?

A:

- Not recommended to communicate directly between two Fragments as this creates a tight coupling between them and reduces their reusability

- Use the hosting Activity as a mediator for communication between Fragments
  - E.g., use an interface and the hosting Activity
    - Define a communication interface in the sender Fragment
    - Declare a reference to the interface in the sender Fragment and ensure the hosting Activity implements the interface during the `onAttach` lifecycle method
    - Implement the interface in the hosting Activity
    - In the sender Fragment, call the interface method to pass data or trigger an action in the receiver Fragment
    - In the receiver Fragment, create a method to receive the data or action from the sender Fragment

## Fragment Back Stack - Adding vs. Replacing

Q: What is the difference between adding and replacing a Fragment in the back stack?

A: Adding and-or replacing a Fragment in the back stack pertains to how you manage Fragments during a transaction using the `FragmentManager`. Both actions are used to manage the `Fragment` lifecycle and navigation, but they have different effects on the back stack and Fragment behavior

- Adding a Fragment to the back stack
  - Attaches a new Fragment to the existing container without removing or hiding the current Fragment
  - Places the "new" Fragment on top of the "current" Fragments &rarr; Both Fragments will coexist in the same container
  - When the user presses the back button, the "new" Fragment will be removed and the previous ("current") Fragment will be visible (as it was never removed from the container)
  - Fragment transaction is added to the back stack &rarr; Allows the `FragmentManager` to manage the navigation history

- Replacing a Fragment in the back stack
  - Removes the current Fragment from the container and adds a new Fragment in its place
  - Replaced Fragment gets destroyed and its view hierarchy will be removed from the container
  - Replace transaction
    - If added to the back stack, then when the user presses the back button, the removed Fragment will be recreated and displayed again, restoring its previous state
    - If not added to the back stack, then the removed Fragment will not be recreated when the back button is pressed

## Default Constructor and Fragment Creation

Q: Why is it recommended to only use the default constructor to create a Fragment?

A:

- It is recommended to only use the default (parameterless) constructor to create a Fragment because of how the Android system manages the Fragment lifecycle, particularly when it comes to handling configuration changes (e.g., a screen rotation) or low-memory situations

- Configuration change occurs or the system faces low-memory situations
  - Android system destroys and recreates the Activity and its associated Fragments
  - Android system uses the default constructor to recreate the Fragment instances
  - With a Fragment that uses a custom constructor that takes arguments, the arguments will not be present when the system recreates the Fragment using the default constructor &rarr; Fragment will lose any data or state information passed through the custom constructor, which may lead to crashes or unexpected behavior in the app

- Use a companion object with a factory method and a Bundle to pass data to the Fragment
  - Android system can properly manage the Fragment lifecycle &rarr; Preserve state across configuration changes and low-memory situations while still passing necessary data to the Fragment

## Configuration Change

Q: What happens when an Android device rotates?

A: When an Android device rotates, the screen orientation changes, which triggers a configuration change. The configuration change causes the following sequence of events:

- The currently running Activity is destroyed, releasing any resources it holds and ensuring a clean slate for the new instance of the Activity
  - Android calls the following methods `onPause()`, then `onStop()`, and finally `onDestroy()`
- A new instance of the Activity is created to adapt to the new screen orientation
  - Android calls the following methods `onCreate()`, then `onStart()`, and finally `onResume()`
- Views and resources are reloaded to fit the new orientation
  - May include using alternative layouts, dimensions, or drawables that better suit the new screen configuration
- State (e.g., user input, scroll position, etc.) restoration
  - Use the `onSaveInstanceState()` method to save the Activity's state in a Bundle before the destruction process, then restore the state in the new instance of the Activity by passing the Bundle to the `onCreate()` method

Configuration changes can be resource-intensive
- Can choose to handle configuration changes manually by declaring the `android:configChanges` attribute for the corresponding Activity in the AndroidManifest.xml file &rarr; Prevents the Activity from being destroyed and recreated but requres updating the layout and resources manually in the `onConfigurationChanged()` method

## `onCreate()` vs. `onStart()`

Q: What is the difference between `onCreate()` and `onStart()`?

A:

- Summary
  - `onCreate()` is called when the Activity is first created and is used for one-time setup and configuration tasks
  - `onStart()` is called each time the Activity becomes visible after being stopped or initially launched

- The difference between `onCreate()` and `onStart()` is the purpose each serves and the different points they are called in the lifecycle

- `onCreate()`
  - Called when the Activity is first created
    - Should perform initial setup and one-time configuration for the Activity, e.g., setting the content view, initializing UI components, and setting up data binding or event listeners
  - Receives a `Bundle` object as an argument
    - `Bundle` may contain saved instance state data if the Activity is being recreated after a configuration change or after being destroyed by the system &rarr; Use the saved state to restore the previous state of the Activity
  - Is only called once during the lifecycle of an Activity, unless it is explicitly destroyed and recreated by the system or the app
  - After, the Activity transitions to the "created" state, and `onStart()` (i.e., the next lifecycle method) is called

- `onStart()`
  - Called after `onCreate()` during the initial launch of the Activity
  - Is also called when the Activity becomes visible again after being stopped or obscured by another Activity
  - Should perform tasks that are required each time the Activity becomes visible, such as registering broadcast receivers, starting animations, or updating UI elements based on new data
  - Can be called multiple times during the lifecycle of an Activity as the Activity transitions between the "started" and "stopped" states
  - After, the Activity transitions to the "started" state, and `onResume()` (i.e., the next lifecycle method) is called

## Calling `onDestroy()` Without Calling `onPause()` or `onStop()`

Q: When would `onDestroy()` be called for an Activity without calling `onPause()` and `onStop()`?

A: Only in exceptional cases would `onDestroy()` be called for an Activity without calling `onPause()` and `onStop()`. Specifically:

- Calling `finish()` in `onCreate()`
  - Finishes the Activity during its creation due to some initialization error or condition
  - System calls `onDestroy()` directly without going through the `onPause()` or `onStop()` lifecycle methods
    - Occurs because the Activity has not yet fully started or become visible to the user

- System kills the process hosting the Activity (???)
  - Rare situation where the Android system may decide to kill the entire process hosting the Activity due to extreme low-memory conditions or other critical scenarios
  - Process is terminated immediately and the Activity lifecycle methods, including `onPause()`, `onStop()`, and `onDestroy()` are not called

## `onSavedInstanceState()` and `onRestoreInstanceState()`

Q: What are `onSavedInstanceState()` and `onRestoreInstanceState()` in an Activity?

A:

- `onSavedInstanceState()` &rarr; Used to store data before pausing the Activity

- `onRestoreInstanceState()` &rarr; Uses the received bundle that contains instance state information to recover the saved state of an Activity when the Activity is recreated after destruction

# User Interface Questions

## View

Q: What is `View` in Android?

A: A `View`:

- Is a fundamental building block of the UI
- Represents a rectangular area on the screen that is responsible for drawing and handling user interaction events
- A View/Views are the basic elements used to compose a UI hierarchy in Android applications

- Basically, any UI element on the screen, such as a Button, CheckBox, EditText, etc., is an instance of a View or one of its subclasses
  - The elements listed are pre-built View classes

- View objects can be nested within other View objects to create a View hierarchy
  - Typically done using ViewGroup subclasses like LinearLayout, RelativeLayout, or ConstraintLayout
    - ViewGroup &rarr; A special type of View that can contain and manage other View Objects, thus forming a tree-like structure for the UI

## RelativeLayout vs. LinearLayout

Q: Discuss RelativeLayout vs. LinearLayout

A: RelativeLayout and LinearLayout are two common layout types in Android used to arrange Views in a UI. Each layout type has its own characteristics and use cases.

- RelativeLayout
  - Is a layout in which child Views are positioned relative to each other or the parent layout
  - Allows you to define rules for positioning child Views, such as aligning them to the left, right, top, or bottom of another View or the parent layout. Child Views can also be positioned relative to the center of the parent layout or another View
  - Allows for the creation of complex and flexible layouts without the need for nested layouts, which can improve performance
  - Is more versatile than LinearLayout, but can be more challenging to work with, especially when dealing with a large number of child Views and complex positioning rules

- LinearLayout
  - Is a layout that arranges child Views in a single row or column depending on the orientation attribute
  - Allows the orientation to be set to either horizontal or vertical
  - Is simpler to use than RelativeLayout and is more suitable for straightforward and linear UI designs
  - Might require nested layouts for complex UI designs, which can negatively impact performance

## ConstraintLayout

Q: Discuss ConstraintLayout

A: ConstraintLayout is:

- A powerful and flexible layout manager in Android that allows for the creation of complex and responsive UI designs with ease
- Designed to optimize performance by reducing the need for nested layouts, which can impact rendering times and slow down the app

- Key features:
  - Flat layout hierarchy
    - Minimize the number of nested layouts, resulting in a flatter and more efficient view hierarchy
    - Can lead to improved performance, especially for complex UI designs
  - Flexible positioning and sizing
    - Provides the ability to position and size Views using constraints, which are rules that define the relationship between one View and another, or between a View and the parent layout
    - Create flexible and responsive layouts that can adapt to different screen sizes and orientations
  - Chains and guidelines
    - Helps align and distribute Views evenly or create responsive designs that adapt to different screen sizes
  - Design-time attributes
    - Preview the layout in the Android Studio Layout Editor without affecting the runtime behavior of the app
  - Compatability
    - Available as a support library &rarr; Can be used in Android projects targeting API level 9 (Android 2.3) and above

## `View.GONE` vs `View.INVISIBLE`

Q: What is the difference between `View.GONE` and `View.INVISIBLE`?

A: `View.GONE` and `View.INVISIBLE` are two constants used to control the visibility of a View. They have different effects on the View's appearance and layout behavior:

- `View` visibility set to `View.GONE`
  - `View` is removed from the layout and not drawn on the screen
  - `View` does not occupy any space in the layout and the space it would have taken up is collapsed, which allows other `View`s to fill the space
  - `View` is still part of the hierarchy, but is effectively hidden and does not participate in the layout process

- `View` visibility set to `View.INVISIBLE`
  - `View` is not drawn on the screen but still occupies space in the layout
  - `View` is essentially hidden, but its dimensions are retained and it continues to participate in the layout process (acting as a placeholder)

## Custom View

Q: Can you create a custom View?

A: Yes, you can create a custom View by extending the `View` class or one of its subclasses

- Creating a custom View allows you to implement custom drawing, handle user interaction, and add custom behavior to fit your app's requirements

- Process:
  - Create a new Kotlin class that extends `View` or one of its subclasses
  - Override the `onMeasure()` method to specify how the custom View should be measured
  - Override the `onDraw()` method to implement custom drawing for your view
  - Handle user interaction by overriding methods like `onTouchEvent()`
  - Use the custom view in an XML layout file by using the fully quality class name
  - Additionally, create custom attributes for the View by defining them in the `attrs.xml` file and then retrieving them in the custom View's constructor

# Jetpack

## LiveData vs. ObservableField

Q: How is LiveData different from an ObservableField?

A: LiveData and ObservableField are both used for data binding and observing changes in data, but they have different characteristics and use cases in Android development

- LiveData:
  - Is a lifecycle-aware data holder class that allows for observing changes in data and updating the UI automatically when the data changes
  - Is part of the Android Architecture Components library and is designed to work with ViewModel and other lifecycle-aware components
  - Respects the lifecycle of its observers (e.g., Activities and Fragments) and only updates the UI when the observer is in an active state (i.e., STARTED or RESUMED) &rarr; Helps prevent memory leaks and crashes due to updating the UI when the observer is not active
  - Can be observed by multiple observers and it automatically manages the subscription and unsubscription of observers based on their lifecycle

- ObservableField:
  - Is part of Android's Data Binding library and is used for creating observable objects that can be bound to the UI
  - Is **NOT** lifecycle-aware, meaning it does not automatically manage the subscription and unsubscription of observers based on their lifecycle &rarr; Can lead to memory leaks or crashes if not handled carefully
  - Provides a simple way to create observable properties in the data models or ViewModel, but does not have built-in lifecycle management like LiveData
  - Can be observed by multiple observers, but requires the developer to manage the observers' lifecycle and unsubscription

# Other Questions

## Image Loading

- Q: How would you handle image loading?

- A: There are several methods to load images, ranging from using built-in Android APIs to employing third-party libraries.

- Android's built-in APIs:
  - BitmapFactory
    - Use the BitmapFactory class to decode images from resources, assets, or local storage
    - Note: Directly decoding large images can lead to OutOfMemoryError &rarr; Avoid by decoding the image bounds, calculate the appropriate sample size for the target ImageView, and then decode the scaled-down version of the image
<br></br>
- Using third-party libraries
  - Recommended for most use cases as they simplify image loading, improve performance, and help avoid common pitfalls such as memory leaks or OutOfMemoryError
  - Glide
    - A fast and efficient open-source media management and image loading library developed by Google
    - Can load images from various sources, including network, local storage, and resources
    - Handles caching, memory management, and image transformations
  - Picasso
    - Powerful open-source image downloading and caching library developed by Square
    - Simplifies image loading by handling complex image processing, caching, and memory management tasks

## Networking

- Q: How would you handle networking?

- A: There are several methods to perform network operations, ranging from built-in Android APIs to employing third-party libraries.

- Android's built-in APIs:
  - HttpURLConnection
    - Built-in Java class that can be used for basic HTTP networking tasks like GET and POST requests
    - Lightweight and suitable for simpler use cases
    - May require manual handling for advanced features like retries or timeouts
  - AsyncTask
    - Used to perform network operations on a background thread
    - Has limitations, such as handling configuration changes poorly and potential memory leaks
    - Less recommended for modern Android development
<br></br>
- Using third-party libraries
  - Retrofit
    - Popular and powerful open-source library developed by Square for handling HTTP requests and parsing responses
    - Uses annotations to define API endpoints and automatically converts JSON responses into (Java) objects
    - Can be used with various HTTP client libraries like OkHttp and supports pluggable converters for different serialization formats
  - OkHttp
    - Powerful and efficient HTTP client library developed by Square
    - Provides advanced features like connection pooling, transparent GZIP compression, response caching, and automatic retries
    - Can be used as a standalone library or in combination with Retrofit for a more comprehensive solution

# Questions from Past Interviews

## WillowTree

1. **Coroutines:** Coroutines are a Kotlin feature that converts async callbacks into sequential code, making the code more readable and simpler. They help manage long-running tasks that might otherwise block the main thread and cause your app to freeze. They're revolutionary because they solve the problem of callback hell and allow you to write cleaner, more manageable code.

2. **Suspend Functions:** Suspend functions are at the heart of coroutines. A function marked with the 'suspend' keyword can be paused and resumed, allowing long-running tasks to be managed more effectively. This means the system won't block the thread it's running on and other operations can use the thread.

3. **Flows:** In Kotlin, `Flow` is a type that can emit multiple values sequentially, making it useful for handling stream of data asynchronously. Similar to how `LiveData` works on Android, `Flow` offers more flexibility and control.

4. **Dependency Injection:** Dependency Injection (DI) is a technique where an object receives its dependencies from outside. It increases the flexibility, testability and maintainability of your code. On Android, DI libraries like Dagger, Hilt or Koin are commonly used.

5. **ProGuard:** ProGuard is a tool that shrinks, optimizes, and obfuscates your code by removing unused code and renaming classes, fields, and methods with semantically obscure names, making the APK harder to reverse engineer.

6. **RecyclerView vs ListView:** `RecyclerView` is a more advanced version of `ListView` with improved performance and greater flexibility. It was introduced as part of the material design guidelines. Key benefits of `RecyclerView` include the built-in layout manager for item arrangement, item animator for animations, and view holder pattern for recycling items.

7. **ViewModel:** `ViewModel` is part of Android Architecture Components, which are libraries that help you design robust, testable, and maintainable apps. `ViewModel` stores and manages UI-related data in a lifecycle-conscious way - it's designed to store UI-related data so that the data survives configuration changes like screen rotations.

8. **Repository Pattern:** The Repository pattern is a design pattern that abstracts the data layer, providing a way to access data from various sources like network, database, etc. It provides a clean API for data access to the rest of the application.

9. **JSON:** JSON (JavaScript Object Notation) is a lightweight data-interchange format that's easy for humans to read and write and easy for machines to parse and generate. On Android, you commonly interact with JSON when consuming REST APIs or storing structured data.

10. **Google's App Architecture:** Google's recommended app architecture suggests designing the app with a layered approach. The UI layer interacts with ViewModel, ViewModel fetches data from the Repository, and Repository decides whether to fetch data from a local database or network. This architecture encourages the Single Responsibility Principle and separation of concerns, making the app easier to maintain and test. Components like ViewModel, LiveData, Room, and DataBinding are recommended to build the architecture.

## Anywhere Real Estate

1. **Null Safety:** Kotlin incorporates inherent null safety. This means that Kotlin types by default can't hold null values, helping to eliminate the risk of Null Pointer Exceptions. You can, however, declare a variable as nullable by adding a "?" after the type.

2. **Exception Handling:** Kotlin uses a `try-catch-finally` approach, similar to Java, for exception handling. However, unlike Java, Kotlin doesn't have checked exceptions, meaning the compiler doesn't force you to catch or declare any exceptions.

3. **Interfaces:** Kotlin interfaces are similar to Java's, serving as contracts that can be implemented by classes. They can contain abstract function declarations, as well as function implementations, but they can't hold state (no backing fields).

4. **Annotations:** Annotations in Kotlin provide metadata about your code that can be read by the compiler, the Kotlin runtime, or other tools. They can be used to suppress warnings, generate extra code, or affect the behavior of your code in various ways.

5. **Two-Way Data Binding:** Two-way Data Binding means that the UI fields are bound to ViewModel fields in a way that any changes in ViewModel fields automatically update in the UI, and vice-versa. This is particularly useful when you want user inputs to be automatically reflected in your underlying data model.

6. **SOLID Principles:** SOLID is an acronym for five design principles intended to make software designs more understandable, flexible, and maintainable. They are: Single Responsibility Principle, Open-Closed Principle, Liskov Substitution Principle, Interface Segregation Principle, and Dependency Inversion Principle. While these principles aren't specific to Kotlin, they can and should be applied when writing Kotlin code.

7. **Principle of Least Surprise:** This principle asserts that a system should behave in a manner consistent with how users expect it to behave; in other words, it should meet users' expectations and not surprise them. This principle is applicable to any area of software development, including Android development with Kotlin.

8. **Unit Testing:** Unit testing is a method of testing where individual units of source code, such as functions or methods, are tested to determine whether they work correctly. Kotlin has great support for unit testing. Libraries like JUnit, Mockito, and Robolectric are commonly used, and Kotlin's features such as Coroutines and Flows have their own testing APIs.

9. **MVP Design Pattern:** MVP stands for Model-View-Presenter. It's a software architectural pattern that separates the application into three interconnected parts: Model (handles data), View (displays the UI and triggers user actions), and Presenter (responds to UI actions and updates the data model). This separation facilitates easier testing and maintenance of code.

## More Anywhere Real Estate

Sure, let's go through each SOLID principle and how it applies to Android development in Kotlin:

1. **Single Responsibility Principle (SRP):** This principle states that a class should have one, and only one, reason to change. In Android development, this could mean separating data management, UI logic, and business logic into separate classes. For example, a `ViewModel` should be responsible for preparing data for the UI but should not be responsible for fetching data from the network or a database.

2. **Open-Closed Principle (OCP):** This principle states that software entities should be open for extension but closed for modification. This encourages the use of abstract classes and interfaces in Kotlin for Android development. For example, you can define a `DatabaseInterface` and implement it with `RoomDatabaseClass`. If you later decide to switch databases, you just need to provide a new implementation of the `DatabaseInterface`.

3. **Liskov Substitution Principle (LSP):** This principle asserts that subclasses must be substitutable for their base classes without causing issues. This principle helps when designing inheritance hierarchies in your Android app, and helps maintain a proper, logical inheritance hierarchy.

4. **Interface Segregation Principle (ISP):** This principle states that clients should not be forced to depend upon interfaces they do not use. In other words, it's better to have many smaller, role-specific interfaces, rather than one large, general-purpose interface. For example, if a class only needs to load data, don't give it an interface that includes saving and deleting data methods.

5. **Dependency Inversion Principle (DIP):** This principle states that high-level modules should not depend on low-level modules - both should depend on abstractions. Furthermore, abstractions should not depend upon details - details should depend upon abstractions. In the context of Android development with Kotlin, this principle supports the use of dependency injection, which makes classes more modular, easier to test, and better suited for collaboration with others.

Regarding unit tests in Kotlin for Android, a typical unit test might look like this:

```kotlin
@RunWith(JUnit4::class)
class ExampleUnitTest {

    private lateinit var systemUnderTest: SystemUnderTest

    @Before
    fun setup() {
        // Initialization work happens here.
        systemUnderTest = SystemUnderTest()
    }

    @Test
    fun `should return correct result when condition is met`() {
        // Arrange
        val expected = ...

        // Act
        val result = systemUnderTest.performAction()

        // Assert
        assertEquals(expected, result)
    }

    @After
    fun tearDown() {
        // Clean up work happens here.
    }
}
```

In this example:

- `@RunWith(JUnit4::class)` is an annotation to specify the test runner.
- `@Before` and `@After` are annotations indicating methods to be run before and after each test, usually for setup and cleanup.
- `@Test` is an annotation indicating that the method is a test method.
- The test name is a descriptive sentence indicating what the test is for.
- The body of the test follows the Arrange-Act-Assert pattern.

Remember, the purpose of unit testing is to verify the correctness of a unit of work (a function or method), and each unit test should test only one specific aspect of the system under test.
