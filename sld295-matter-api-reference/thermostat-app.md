# Thermostat Application Override APIs

To override any of the following hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches the declaration in `autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback, sets the LCD UI, and initializes the thermostat. |
| `InitThermostatImpl` | `InitThermostat` | Initializes the sensor, UI, and periodic temperature sampling. |
| `InitSensorImpl` | `InitSensor` | Initializes the hardware temperature sensor if it is present. |
| `GetTemperatureImpl` | `GetTemperature` | Reads the Si70xx sensor if it is present; otherwise, provides a simulated temperature. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Routes function-button events to the base application handler. |
| `SensorTimerEventHandlerImpl` | `SensorTimerEventHandler` | Posts an application event to update the temperature when the sensor timer expires. |
| `TemperatureUpdateEventHandlerImpl` | `TemperatureUpdateEventHandler` | Samples the temperature and updates the Thermostat `LocalTemperature` attribute. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Handles attribute changes from the Thermostat cluster and monitors attribute changes from the Identify cluster. |
| `DMThermostatClusterInitImpl` | `DMThermostatClusterInit` | Installs the default Thermostat delegate on an endpoint. |
