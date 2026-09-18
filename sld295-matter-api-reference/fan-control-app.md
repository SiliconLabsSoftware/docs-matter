# Fan Control Application Override APIs

To override any of the following hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches the declaration in `autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback, initializes fan control, and updates the display. |
| `InitFanControlImpl` | `InitFanControl` | Installs Fan Control delegates, initializes the LED, and applies the initial attribute state. |
| `HandleStepImpl` | `HandleStep` | Handles a Fan Control Step command by updating speed or percentage settings. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Routes function button events to the base application handler. |
| `FanUiUpdateEventHandlerImpl` | `FanUiUpdateEventHandler` | Updates the fan LED and, when enabled, the display. |
| `HandleFanModeChangeImpl` | `HandleFanModeChange` | Synchronizes speed and percentage settings after a change to FanMode. |
| `DeriveFanModeFromPercentImpl` | `DeriveFanModeFromPercent` | Maps PercentSetting to Off, Low, Medium, or High fan mode. |
| `HandlePercentSettingChangeImpl` | `HandlePercentSettingChange` | Updates PercentCurrent after PercentSetting changes. |
| `HandleSpeedSettingChangeImpl` | `HandleSpeedSettingChange` | Updates SpeedCurrent after SpeedSetting changes. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Applies changes to the Fan Control PercentSetting, SpeedSetting, and FanMode attributes and logs Identify changes. |
