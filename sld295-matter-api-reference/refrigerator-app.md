# Refrigerator application override APIs

Override each hook below by declaring the `*Impl()` method in `CustomerAppTask.h`
and implementing it in `CustomerAppTask.cpp`. Match the signature in
`autogen/AppTaskImpl.h`. The public `Init()` method maps to
`CabinetModeInitImpl()`, not `InitImpl()`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Register the button callback and initialize the refrigerator. |
| `InitRefrigeratorImpl` | `InitRefrigerator` | Configure refrigerator endpoint composition, semantic tags, and the Temperature Control delegate. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Route function button events to the base application handler. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Handle Refrigerator Alarm and Temperature Control changes and observe Identify changes. |
| `CabinetModeClusterInitImpl` | `CabinetModeClusterInit` | Construct and initialize the `ModeBase::Instance` for the Cabinet Mode cluster on the refrigerator endpoint. |
| `CabinetModeInitImpl` | `Init` | Return success. The Cabinet Mode delegate has no additional default initialization. |
| `HandleChangeToModeImpl` | `HandleChangeToMode` | Accept the requested Cabinet Mode, except a direct transition between Normal and Rapid Freeze. |
| `GetModeLabelByIndexImpl` | `GetModeLabelByIndex` | Return the supported Cabinet Mode label at the given index. |
| `GetModeValueByIndexImpl` | `GetModeValueByIndex` | Return the supported Cabinet Mode value at the given index. |
| `GetModeTagsByIndexImpl` | `GetModeTagsByIndex` | Return the semantic tags for the supported Cabinet Mode at the given index. |
