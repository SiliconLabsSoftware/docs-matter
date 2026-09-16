# Fan Control application override APIs

Override each hook below by declaring the `*Impl()` method in `CustomerAppTask.h`
and implementing it in `CustomerAppTask.cpp`. Match the signature in
`autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Register the button callback, initialize fan control, and update the display. |
| `InitFanControlImpl` | `InitFanControl` | Install Fan Control delegates, initialize the LED, and apply the initial attribute state. |
| `HandleStepImpl` | `HandleStep` | Handle a Fan Control Step command by updating speed or percentage settings. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Route function button events to the base application handler. |
| `FanUiUpdateEventHandlerImpl` | `FanUiUpdateEventHandler` | Update the fan LED and, when enabled, the display. |
| `HandleFanModeChangeImpl` | `HandleFanModeChange` | Synchronize speed and percentage settings after a FanMode change. |
| `DeriveFanModeFromPercentImpl` | `DeriveFanModeFromPercent` | Map PercentSetting to Off, Low, Medium, or High fan mode. |
| `HandlePercentSettingChangeImpl` | `HandlePercentSettingChange` | Update PercentCurrent after PercentSetting changes. |
| `HandleSpeedSettingChangeImpl` | `HandleSpeedSettingChange` | Update SpeedCurrent after SpeedSetting changes. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Apply Fan Control PercentSetting, SpeedSetting, and FanMode changes, and log Identify changes. |
