### ViewModels and Models with Jetpack Compose.

Here's a simple counter example that demonstrates how to use ViewModels and Models to manage state in a Compose-based Android app:

1. Define the Model:

```kotlin
data class CounterModel(val count: Int = 0)
```

The `CounterModel` is a simple data class that represents the state of our counter. It has a single property `count` initialized to 0.

2. Create the ViewModel:

```kotlin
class CounterViewModel : ViewModel() {
    private val _counterState = mutableStateOf(CounterModel())
    val counterState: State<CounterModel> = _counterState

    fun incrementCounter() {
        _counterState.value = _counterState.value.copy(count = _counterState.value.count + 1)
    }

    fun decrementCounter() {
        _counterState.value = _counterState.value.copy(count = _counterState.value.count - 1)
    }
}
```

The `CounterViewModel` is responsible for managing the state of the counter. It uses the `mutableStateOf` function from Compose to create a mutable state holder for the `CounterModel`. The `counterState` is exposed as a read-only `State` to the composable.

The `incrementCounter()` and `decrementCounter()` methods update the `count` value of the `CounterModel` by creating a new copy with the updated count.

3. Create the Composable:

```kotlin
@Composable
fun CounterScreen(viewModel: CounterViewModel = viewModel()) {
    val counterState by viewModel.counterState

    Column(
        modifier = Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text(
            text = "Count: ${counterState.count}",
            style = MaterialTheme.typography.h4
        )
        Spacer(modifier = Modifier.height(16.dp))
        Row {
            Button(onClick = { viewModel.decrementCounter() }) {
                Text("Decrement")
            }
            Spacer(modifier = Modifier.width(16.dp))
            Button(onClick = { viewModel.incrementCounter() }) {
                Text("Increment")
            }
        }
    }
}
```

The `CounterScreen` composable function represents the UI of our counter screen. It takes an instance of `CounterViewModel` as a parameter, which is provided by the `viewModel()` function from the `androidx.lifecycle.viewmodel.compose` package.

Inside the composable, we use the `by` delegate to observe the `counterState` from the ViewModel. Whenever the state changes, the composable is recomposed to reflect the updated state.

The composable displays the current count value using a `Text` composable and provides two buttons to increment and decrement the count by calling the respective methods from the ViewModel.

With this approach, the state is managed by the ViewModel, and the composable observes the state and updates the UI accordingly. The Model (`CounterModel`) represents the data structure of the state, and the ViewModel handles the business logic and state updates.

This example demonstrates a simple and effective way to manage state using ViewModels and Models in a Compose-based Android app. You can extend this pattern to handle more complex state management scenarios in your app.