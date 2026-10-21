# Refrigerator Application Override APIs

To override any of the following hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches its declaration in `autogen/AppTaskImpl.h`. The public `Init()` method maps to `CabinetModeInitImpl()` rather than `InitImpl()`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback and initializes the refrigerator. |
| `InitRefrigeratorImpl` | `InitRefrigerator` | Configures the refrigerator endpoint composition and semantic tags, and initializes the Temperature Control delegate. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Routes function-button events to the base application handler. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Handles attribute changes from the Refrigerator Alarm and Temperature Control clusters and monitors attribute changes from the Identify cluster. |
| `CabinetModeClusterInitImpl` | `CabinetModeClusterInit` | Constructs and initializes a `ModeBase::Instance` for the Cabinet Mode cluster on the refrigerator endpoint. |
| `CabinetModeInitImpl` | `Init` | Returns a success status. The Cabinet Mode delegate requires no additional initialization by default. |
| `HandleChangeToModeImpl` | `HandleChangeToMode` | Accepts the requested Cabinet Mode unless the request is for a direct transition between Normal and Rapid Freeze. |
| `GetModeLabelByIndexImpl` | `GetModeLabelByIndex` | Returns the supported Cabinet Mode label at the specified index. |
| `GetModeValueByIndexImpl` | `GetModeValueByIndex` | Returns the supported Cabinet Mode value at the specified index. |
| `GetModeTagsByIndexImpl` | `GetModeTagsByIndex` | Returns the semantic tags associated with the supported Cabinet Mode at the specified index. |
