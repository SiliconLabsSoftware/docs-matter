# Air Quality Sensor application override APIs

Override each hook below by declaring the `*Impl()` method in `CustomerAppTask.h`
and implementing it in `CustomerAppTask.cpp`. Match the signature in
`autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Register the button callback, set the LCD UI, and initialize the air quality sensor. |
| `InitAirQualitySensorImpl` | `InitAirQualitySensor` | Create the periodic sensor timer, initialize hardware when present, and start sampling. |
| `GetAirQualityValueImpl` | `GetAirQualityValue` | Read the onboard air quality sensor, or a simulated value if none is present. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Route function button events to the base application handler. |
| `SensorTimerEventHandlerImpl` | `SensorTimerEventHandler` | Read the sensor and schedule an Air Quality attribute update. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Log Identify attribute changes. |
