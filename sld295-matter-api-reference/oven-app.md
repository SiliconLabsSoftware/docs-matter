# Oven Application Override APIs

To override any of the following hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches the declaration in `autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback and initializes the oven, connectivity handler, cooktop LED, and display. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Routes oven-action and function-button events. |
| `OvenButtonHandlerImpl` | `OvenButtonHandler` | Converts an oven button press into a cooktop on/off action. |
| `OvenActionHandlerImpl` | `OvenActionHandler` | Applies an oven or cooktop action and updates the application UI. |
| `ConnectivityEventHandlerImpl` | `ConnectivityEventHandler` | Propagates the cooktop off state after DNS-SD initialization completes. |
| `InitBindingHandlerImpl` | `InitBindingHandler` | Initializes the Binding Manager and registers its command and context release handlers. |
| `CookTopBindingPropagateStateImpl` | `CookTopBindingPropagateState` | Notifies bound OnOff and Fan Control clusters of the cooktop state. |
| `BoundDeviceChangedHandlerImpl` | `BoundDeviceChangedHandler` | Writes the pending cooktop state to a matching bound OnOff or Fan Control peer. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Routes OnOff changes and observes Temperature Control and Identify changes. |
| `OnAttributeChangedImpl` | `OnAttributeChanged` | Converts an Oven Mode `CurrentMode` change into an application event. |
| `DMOvenModeClusterInitCallbackImpl` | `DMOvenModeClusterInitCallback` | Performs no application-specific action by default. |
| `DMOvenModeClusterShutdownCallbackImpl` | `DMOvenModeClusterShutdownCallback` | No default application logic. The Oven Mode cluster shutdown callback does nothing. |
| `InitOvenImpl` | `InitOven` | Initializes the oven endpoints, delegates, binding, supported levels, and initial cluster state. |
| `OnOffAttributeChangeHandlerImpl` | `OnOffAttributeChangeHandler` | Synchronizes the cooktop and cooking-surface states after a change to the OnOff attribute. |
| `IsTransitionBlockedImpl` | `IsTransitionBlocked` | Returns true if the requested Oven Mode transition is in the blocked-transition list. |
