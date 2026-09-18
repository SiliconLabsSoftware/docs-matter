# Base Platform Application Override APIs

To override any of the following hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches the declaration in `autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback, initializes the LED, and shows the demo UI or QR code when enabled. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Routes user-action button events to `ApplicationEventHandler` and function-button events to the base application handler. |
| `ApplicationEventHandlerImpl` | `ApplicationEventHandler` | Toggles the LED when the user-action button is pressed. |
| `OnEnterActiveModeImpl` | `OnEnterActiveMode` | Updates the demo UI when the ICD server enters active mode. Available when `CHIP_CONFIG_ENABLE_ICD_SERVER` is enabled. |
| `OnEnterIdleModeImpl` | `OnEnterIdleMode` | Updates the demo UI when the ICD server enters idle mode. Available when `CHIP_CONFIG_ENABLE_ICD_SERVER` is enabled. |
| `OnTransitionToIdleImpl` | `OnTransitionToIdle` | Logs the transition while the ICD server moves to idle mode. Available when `CHIP_CONFIG_ENABLE_ICD_SERVER` is enabled. |
| `OnICDModeChangeImpl` | `OnICDModeChange` | Logs changes between Short Idle Time (SIT) and Long Idle Time (LIT) operating modes. Available when `CHIP_CONFIG_ENABLE_ICD_SERVER` is enabled. |
