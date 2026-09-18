# Air Quality Sensor Application Override APIs

To override any of the following hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches the declaration in `autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback, configures the LCD UI, and initializes the air quality sensor. |
| `InitAirQualitySensorImpl` | `InitAirQualitySensor` | Creates the periodic sensor timer, initializes the sensor hardware when available, and starts sampling. |
| `GetAirQualityValueImpl` | `GetAirQualityValue` | Reads the value from the onboard air quality sensor. If the sensor is unavailable, returns a simulated value. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Routes function-button events to the base application handler. |
| `SensorTimerEventHandlerImpl` | `SensorTimerEventHandler` | Reads the sensor value and schedules an update to the Air Quality attribute. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Logs changes to the Identify attribute. |
