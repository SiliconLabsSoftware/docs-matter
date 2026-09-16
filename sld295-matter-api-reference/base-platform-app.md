# Base Platform application override APIs

Override each hook below by declaring the `*Impl()` method in `CustomerAppTask.h`
and implementing it in `CustomerAppTask.cpp`. Match the signature in
`autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Register the button callback, initialize the LED, and show the demo UI or QR code when enabled. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Route user action button events to `ApplicationEventHandler` and function button events to the base application handler. |
| `ApplicationEventHandlerImpl` | `ApplicationEventHandler` | Toggle the LED for a user action button press. |
| `OnEnterActiveModeImpl` | `OnEnterActiveMode` | Update the demo UI when the ICD server enters active mode. Available when `CHIP_CONFIG_ENABLE_ICD_SERVER` is enabled. |
| `OnEnterIdleModeImpl` | `OnEnterIdleMode` | Update the demo UI when the ICD server enters idle mode. Available when `CHIP_CONFIG_ENABLE_ICD_SERVER` is enabled. |
| `OnTransitionToIdleImpl` | `OnTransitionToIdle` | Log the transition while the ICD server moves to idle mode. Available when `CHIP_CONFIG_ENABLE_ICD_SERVER` is enabled. |
| `OnICDModeChangeImpl` | `OnICDModeChange` | Log the change between SIT and LIT operating modes. Available when `CHIP_CONFIG_ENABLE_ICD_SERVER` is enabled. |
