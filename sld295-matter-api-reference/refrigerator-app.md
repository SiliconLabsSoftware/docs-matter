# Refrigerator Application Override APIs

To override any of the following hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches the declaration in `autogen/AppTaskImpl.h`. The public `Init()` method maps to
`CabinetModeInitImpl()`, not `InitImpl()`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback and initializes the refrigerator. |
| `InitRefrigeratorImpl` | `InitRefrigerator` | Configures refrigerator endpoint composition, semantic tags, and the Temperature Control delegate. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Routes function button events to the base application handler. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Handles Refrigerator Alarm and Temperature Control changes and observes Identify changes. |
| `CabinetModeClusterInitImpl` | `CabinetModeClusterInit` | Constructs and initializes the `ModeBase::Instance` for the Cabinet Mode cluster on the refrigerator endpoint. |
| `CabinetModeInitImpl` | `Init` | Returns success. The Cabinet Mode delegate has no additional default initialization. |
| `HandleChangeToModeImpl` | `HandleChangeToMode` | Accepts the requested Cabinet Mode, except a direct transition between Normal and Rapid Freeze. |
| `GetModeLabelByIndexImpl` | `GetModeLabelByIndex` | Returns the supported Cabinet Mode label at the given index. |
| `GetModeValueByIndexImpl` | `GetModeValueByIndex` | Returns the supported Cabinet Mode value at the given index. |
| `GetModeTagsByIndexImpl` | `GetModeTagsByIndex` | Returns the semantic tags for the supported Cabinet Mode at the given index. |
