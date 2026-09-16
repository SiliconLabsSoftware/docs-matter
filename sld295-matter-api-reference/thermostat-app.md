# Thermostat application override APIs

Override each hook below by declaring the `*Impl()` method in `CustomerAppTask.h`
and implementing it in `CustomerAppTask.cpp`. Match the signature in
`autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Register the button callback, set the LCD UI, and initialize the thermostat. |
| `InitThermostatImpl` | `InitThermostat` | Initialize the sensor, UI, and periodic temperature sampling. |
| `InitSensorImpl` | `InitSensor` | Initialize the hardware temperature sensor when present. |
| `GetTemperatureImpl` | `GetTemperature` | Read the Si70xx sensor when present, otherwise supply a simulated temperature. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Route function button events to the base application handler. |
| `SensorTimerEventHandlerImpl` | `SensorTimerEventHandler` | Post a temperature update application event when the sensor timer expires. |
| `TemperatureUpdateEventHandlerImpl` | `TemperatureUpdateEventHandler` | Sample temperature and update the Thermostat `LocalTemperature` attribute. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Handle Thermostat changes and observe Identify changes. |
| `DMThermostatClusterInitImpl` | `DMThermostatClusterInit` | Install the default Thermostat delegate for an endpoint. |
