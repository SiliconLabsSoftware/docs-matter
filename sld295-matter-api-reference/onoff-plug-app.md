# On/Off Plug application override APIs

Override each hook below by declaring the `*Impl()` method in `CustomerAppTask.h`
and implementing it in `CustomerAppTask.cpp`. Match the signature in
`autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Register the button callback, initialize the plug, LED, and display. |
| `InitPlugImpl` | `InitPlug` | Read the OnOff attribute into the plug on/off state. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Route plug action and function button events. |
| `OnOffActionEventHandlerImpl` | `OnOffActionEventHandler` | Toggle the plug and synchronize its OnOff attribute for a button event. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Handle OnOff, Level Control, and Identify attribute changes. |
