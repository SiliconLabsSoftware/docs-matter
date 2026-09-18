# On/Off Plug Application Override APIs

To override any of the following hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches the declaration in `autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback and initializes the plug, LED, and display. |
| `InitPlugImpl` | `InitPlug` | Reads the OnOff attribute into the plug On/Off state. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Routes plug-action and function-button events. |
| `OnOffActionEventHandlerImpl` | `OnOffActionEventHandler` | Toggles the plug and synchronizes its OnOff attribute for a button event. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Handles OnOff, Level Control, and Identify attribute changes. |
