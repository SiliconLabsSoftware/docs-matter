# Thermostat Application Override APIs

To override any of the following hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches the declaration in `autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback, sets the LCD UI, and initializes the thermostat. |
| `InitThermostatImpl` | `InitThermostat` | Initializes the sensor, UI, and periodic temperature sampling. |
| `InitSensorImpl` | `InitSensor` | Initializes the hardware temperature sensor when present. |
| `GetTemperatureImpl` | `GetTemperature` | Reads the Si70xx sensor when present, otherwise supplies a simulated temperature. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Routes function button events to the base application handler. |
| `SensorTimerEventHandlerImpl` | `SensorTimerEventHandler` | Posts a temperature update application event when the sensor timer expires. |
| `TemperatureUpdateEventHandlerImpl` | `TemperatureUpdateEventHandler` | Samples temperature and updates the Thermostat `LocalTemperature` attribute. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Handles Thermostat changes and observes Identify changes. |
| `DMThermostatClusterInitImpl` | `DMThermostatClusterInit` | Installs the default Thermostat delegate for an endpoint. |
