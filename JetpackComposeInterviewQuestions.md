1. **How to setup Compose in a new Android app?**
   
    - Open Android Studio and create a new project
    - Choose "Empty Compose Activity" from the list of activity templates
    - Android Studio will setup everything for Jetpack Compose automatically
<br></br>

2. **How to setup Compose in an existing app?**
   
    - Add these lines in your `build.gradle` file:
<br></br>
    ```
    dependencies {
        implementation "androidx.compose.ui:ui:<version>"
        implementation "androidx.compose.material:material:<version>"
        implementation "androidx.compose.ui:ui-tooling:<version>"
    }

    kotlinOptions {
        jvmTarget = '1.8'
        useIR = true
    }

    composeOptions {
        kotlinCompilerExtensionVersion compose_version
        kotlinCompilerVersion '1.5.10'
    }
    ```

    - Replace `<version>` with the version number of Compose you want to use.
<br></br>

3. **What is the difference between Compose UI and Android View?**

    - Android View is a traditional, imperative, and object-oriented system that was the backbone of Android UI development. Android View made it challenging to maintain large apps, and XML files were required for layout design.

    - Compose is a declarative, component-oriented system and a modern toolkit for building native Android UI. Compose simplifies UI development, making UI code concise and intuitive. No XML is required.
<br></br>

4. **What is `setContent()`?**

    - `setContent` is a function provided by the Compose library
    - Used in activities instead of `setContentView` to set the UI for the activity
    - Write your composable functions that describe your UI in the `setContent` block
<br></br>

5. **What are Composable functions?**

    - Composable functions are the building blocks of your UI in Jetpack Compose
    - Composable functions are regular Kotlin functions, but are annotated with the `@Composable` annotation
    - Composable functions describe your UI and can be combined and reused to build your app
<br></br>

6. **What is the lifecycle of a Compose function?**

    - The lifecycle of a Compose function is managed by the Compose runtime
    - Composable functions don't have lifecycle callbacks like `onCreate`, `onDestroy` etc.
    - Composable functions are called to draw the UI and can be called multiple times by the system when the state they read changes or to draw the UI
<br></br>

7. **What is Recomposition?**

    - Recomposition is a phase in Compose where composable functions are re-invoked to reflect new state changes in the UI
    - The system intelligently updates only the part of the UI that depends on the changed state, improving efficiency
<br></br>

8. **What is @Composable?**

    - `@Composable` is an annotation in Jetpack Compose used to indicate that a function is a composable function
    - Composable functions are the building blocks of your UI and can call other composable functions
<br></br>

9. **What is `Modifier` and where would you use it?**

    - `Modifier` in Jetpack Compose is a concept that allows you to modify the composable's appearance or behavior
    - `Modifier` can be used for various things like setting padding, background color, click events, etc.
<br></br>

10. **What are the core UI elements in Compose?**

    - Some of the core UI elements in Jetpack Compose include:
      - `Text` for displaying text
      - `Button` for clickable buttons
      - `Image` for displaying images
      - `TextField` for text input
      - `Surface` for backgrounds and containers
      - Etc.
<br></br>

11. **What layouts are available in Compose?**

    - Some layouts available in Compose include `Column`, `Row`, `Box`, and `Surface` for basic layout structures
    - More complex layouts include `ConstraintLayout` and `LazyColumn`/`LazyRow` for scrolling lists
<br></br>

12. **Can we mix Compose and Android View in a single app?**

    - Yes, Compose can co-exist with traditional Android Views in the same app
    - You can use `ComposeView` in your existing view hierarchy or use `AndroidView` in your composable functions to include traditional Android views
<br></br>

13. **How do we apply themes in a Compose app?**

    - Themes in Compose can be applied using the `MaterialTheme` composable
    - You can define your colors, typography, and shapes in a `Theme.kt` file and apply these themes throughout your app using `MaterialTheme`
<br></br>

14. **What is State in Compose?**

    - State in Compose is data that can change over time
    - When the State changes, the UI recomposes to reflect the new State
    - State can be created using `mutableStateOf` and read in composable functions
<br></br>

15. **What is the `remember` method?**

    - `remember` is a function provided by the Compose runtime that creates a mutable state and remembers its current value across recompositions
<br></br>

16. **What is Side Effect? How many Side Effects are there in Compose?**

    - Side Effects in Jetpack Compose are operations that interact with the outside world, such as reading from or writing to mutable memory
    - There are multiple types of Side Effects in Compose, like `remember`, `onCommit`, `DisposableEffect`, and others
<br></br>

17. **What is the difference between `LaunchedEffect` vs `DisposableEffect`?**

    - `LaunchedEffect` is used to handle Side Effects that might have a suspend function call, such as network calls or database access
    - `DisposableEffect` is used to perform clean-up actions when the composable leaves the composition
<br></br>

18. **What is `rememberCoroutineScope` and what is its use?**

    - `rememberCoroutineScope` is a function that gives you a `CoroutineScope` tied to the lifecycle of the calling composable
    - This scope will be canceled when the composable leaves the composition
<br></br>

19. **How do we access coroutines inside Compose functions?**

    - You can access coroutines inside composable functions by using `rememberCoroutineScope`
    - `rememberCoroutineScope` provides a `CoroutineScope` that is lifecycle aware
<br></br>

20. **How do we handle Exceptions in Compose functions?**

    - Exception handling in Compose functions can be done using try-catch blocks
    - Exceptions thrown inside a composable won't crash your app, but will propagate up to the nearest `CompositionLocalProvider` or the Composition's `CoroutineExceptionHandler`
<br></br>

21. **How does Navigation work in Compose?**

    - Navigation in Jetpack Compose can be implemented using the `navigation-compose` library
    - You define your navigation graph using `NavHost` and `NavGraphBuilder`, where you specify your routes and associated composables
<br></br>

22. **How do we create Navigation, Navigation Graph, and Nested Navigation Graph in Compose?**

    - You create a navigation graph in Compose using `NavHost` and `NavGraphBuilder`
    - Nested graphs can be created using `NavGraphBuilder`'s `navigation` function
<br></br>

23. **What is @Preview?**

    - `@Preview` is an annotation in Compose that allows you to preview your composable functions in Android Studio's preview pane without needing to run the app
<br></br>

24. **How do we create a List View in Compose?**

    - You can create a List View in Compose using `LazyColumn` for vertical lists or `LazyRow` for horizontal lists
    - Inside `LazyColumn` and-or `LazyRow`, you use `items` to define the data and how each item should be represented in the UI
<br></br>

25. **How do we handle lifecycle events in Compose functions?**

    - Handle lifecycle events using effects like `LaunchedEffect` and `DisposableEffect`
    - E.g., you can start a coroutine in `LaunchedEffect` that gets canceled when the composable leaves the composition, or clean up resources using `DisposableEffect`
<br></br>

26. **What are Semantics?**

    - Semantics in Compose are properties that give meaning to your UI
    - Semantics are used to communicate the state and behavior of your UI to accessibility services and for UI testing

27. **What is State Hoisting?**

    - State Hoisting in Compose is a pattern where the state is managed outside the composable that uses it, making the composable stateless and more reusable
    - The hoisted state is then passed to the composable as a parameter
<br></br>

28. **What is the UDF (Unidirectional Data Flow) Pattern?**

    - Unidirectional Data Flow (UDF) is a design pattern where data flows in a single direction, making the state predictable
    - In the context of Compose, this means that state is typically flowed down from parent composables to child composables, and events are propagated up from children to parents
<br></br>

29. **What are the Jetpack Compose Phases?**

    - There are three main phases in the Jetpack Compose: Composition, Layout, and Draw
    - In the Composition phase, composable functions are called to create a tree of composable nodes
    - In the Layout phase, positions and sizes are calculated
    - In the Draw phase, the UI is drawn on the screen
<br></br>

30. **How do we create custom layouts in Compose?**

    - Custom layouts in Compose can be created using the `Layout` or `Measureable` APIs
    - You define how your children should be measured and positioned in your layout
<br></br>

31. **How do we handle State for device orientation changes in Compose UI?**

    - State can be persisted across configuration changes, like device orientation changes, by using `rememberSaveable` instead of `remember`
    - When using `rememberSaveable`, the state will automatically be saved and restored
<br></br>

32. **How do we observe Flows and LiveData States in Compose UI?**

    - Flows and LiveData can be observed in Compose using `collectAsState`
    - The `collectAsState` function collects the data from the Flow or LiveData and provides a State that can be used in your composable
<br></br>

33. **How do we handle back press functionality from a Compose screen?**

    - Back press functionality can be handled in Compose using the `BackHandler` composable from the `androidx.activity.compose` package
    - You provide a callback to be invoked when the back button is pressed
<br></br>

34. **How do We Use Window Insets in Compose?**

    - Window insets in Compose can be obtained using the `rememberInsetsPaddingValues` function from the `accompanist-insets` library
    - The `rememberInsetsPaddingValues` function provides `PaddingValues` that can be applied to your composables to account for system UI overlays
<br></br>

35. **What are `systemBarPadding()` and `navigationBarPadding()` in Compose?**

    - `systemBarPadding` and `navigationBarPadding` are functions provided by the `accompanist-insets` library to apply padding to your composable equal to the size of the system bars or navigation bar
<br></br>

36. **How do we handle accessibility in Compose?**

    - Accessibility in Compose is handled through Semantics
    - You can use the `Modifier.semantics` function to provide properties like `contentDescription`, `stateDescription`, etc. to your composables
<br></br>

37. **How do we write UI test cases for a Compose screen?**

    - UI tests for Compose can be written using the `compose-test-junit` library
    - You can use functions like `onNodeWithText`, `onNodeWithTag`, etc. to find nodes and perform assertions or interactions
<br></br>

38. **How do we write animation in Compose?**

    - Animations in Compose can be created using the `animate*AsState` or `animate*` functions provided by the `compose-animation` library
    - You define your starting and ending values and the system will animate the changes for you.
<br></br>

39. **How do we share data between Composables?**

    - Data can be shared between composables by passing it down as parameters or using `CompositionLocal`
    - If the data is mutable, it can be shared using state and the state hoisting pattern
<br></br>

40. **What is `CompositionLocal`?**

    - `CompositionLocal` is a way to implicitly pass data through the composition tree
    = `CompositionLocal` is similar to `Context` in traditional Android development, and is used for data that's needed by many composables or that cannot be passed down as parameters
<br></br>

# Jetpack Compose Activity and Fragment Lifecycles

- In Jetpack Compose, Activity and Fragment lifecycles still exist, but the emphasis has shifted to the lifecycles of composable functions.

- Activity Lifecycle with Jetpack Compose:
  - An activity still follows the traditional lifecycle: onCreate(), onStart(), onResume(), onPause(), onStop(), onDestroy().
  - In the onCreate() method, we typically call setContent { } to define our composable UI hierarchy.
  - In terms of Jetpack Compose, Activity lifecycle callbacks are not typically where you would handle most of your logic, as you would use lifecycle-aware components within your composables instead.

- Fragment Lifecycle with Jetpack Compose:
  - Fragments also still follow their traditional lifecycle: onAttach(), onCreate(), onCreateView(), onActivityCreated(), onStart(), onResume(), onPause(), onStop(), onDestroyView(), onDestroy(), and onDetach().
  - Similarly to Activities, in the onCreateView() or onViewCreated() method, you'd call setContent { } to set up your composable UI.
  - Like Activities, you would not typically use Fragment lifecycle callbacks to handle logic for composables, but would instead rely on lifecycle-aware components within the composables themselves.

- Composable Lifecycle with Jetpack Compose:
  - Jetpack Compose has its own concept of a lifecycle for composable functions, which is tied to when the composable enters or leaves the composition, and not directly to the Activity or Fragment lifecycle.
  - The lifecycle of a composable function is:
    - Composition: The composable function is first called and included in the composition.
    - Insertion: The produced UI is added to the tree of active composables, and its effects (side-effects introduced by the LaunchedEffect, DisposableEffect and remember functions) are started.
    - Update: If the data the composable reads has changed, the composable will be recomposed - that is, the function will be invoked again to produce a new UI description. Only the effects that depend on changed data will be restarted.
    - Removal: If the composable is no longer needed (for example, because a conditional that included it in the composition has become false), its effects will be stopped, and it will be removed from the tree of active composables.
  - For observing lifecycle events within a composable function, you'd typically use the LaunchedEffect and DisposableEffect functions. The LaunchedEffect function starts a coroutine that's cancelled when the composable leaves the composition, and DisposableEffect starts an effect that produces a Disposable lambda, which is invoked when the composable leaves the composition.
  - For example, you might use LaunchedEffect to start a network request when a composable is first inserted, and use DisposableEffect to cancel ongoing work when the composable is removed.
  - The remember function is also important to the lifecycle of a composable: it creates an object that is remembered across recompositions, as long as the composable remains in the composition. When the composable leaves the composition, the remembered object is forgotten. If the composable is later included in the composition again, the remember function will be called again to create a new object.
  - In summary, while the traditional Android lifecycles still exist when using Jetpack Compose, the key focus shifts to the composable lifecycle, which is more granular and tied to the individual composables rather than the containing Activity or Fragment.