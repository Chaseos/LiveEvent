[![](https://jitpack.io/v/Chaseos/LiveEvent.svg)](https://jitpack.io/#Chaseos/LiveEvent)

Live Event
---
This library holds a class to handle single live events in Android MVVM architectural pattern. This class is extended
form LiveData class, from `androidx.lifecycle:lifecycle-extensions` library, to propagate the data as an event,
which means it emits data just once, not after configuration changes again. Note that event will only be sent 
to active observers, any observers that started observing after the emit won't be notified of the event. 

Usage
---
This source has a sample app where you can find `LiveEventViewModel` in it, in which the `LiveEvent` and/or `LiveEventData` class is used as
follows.
```kotlin
class LiveEventViewModel : ViewModel() {
    private val clickedState = LiveEvent()
    val state: LiveData<Unit> = clickedState
    
    private val clickedDataState = LiveEventData<String>()
    val dataState: LiveData<String> = clickedDataState
    
    private val clickedDataState2 = LiveEventData("event")
    val dataState2: LiveData<String> = clickedDataState2

    fun clicked() {
        clickedState.callEvent() // Main Thread .value call
        clickedState.postEvent() // Any thread post call
        clickedState.throttleEvent() // Main thread .value call with 1000ms throttle (option to pass in millisecond time as Long)
        clickedState.throttlePostEvent() // Any thread post call with 1000ms throttle (option to pass in millisecond time as Long)
        
        clickedDataState.value = ... // Main Thread
        clickedDataState.post(...) // Any thread post call
        clickedDataState.throttleEvent(...) // Main thread .value call with 1000ms throttle (option to pass in millisecond time as Long)
        clickedDataState.throttlePostEvent(...) // Any thread post call with 1000ms throttle (option to pass in millisecond time as 
    }
}
```
