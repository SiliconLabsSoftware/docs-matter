# Multi Sensor Application Override APIs

To override any of the following hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches the declaration in `autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback, initializes the occupancy LED and display, and starts the sensor manager. |
| `InitSensorManagerImpl` | `InitSensorManager` | Initializes the sensor clusters, registers the attribute listener, and schedules periodic sampling. |
| `GetTemperatureAndHumidityImpl` | `GetTemperatureAndHumidity` | Reads the Si70xx sensor if it is present; otherwise, provides simulated temperature and humidity values. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Routes events from the function and occupancy-toggle buttons. |
| `ProcessButtonEventImpl` | `ProcessButtonEvent` | Toggles the Occupancy attribute for an application button event. |
| `TriggerSensorActionImpl` | `TriggerSensorAction` | Samples temperature and humidity and updates their measured value attributes. |
| `OccupancyAttributeUpdateEventImpl` | `OccupancyAttributeUpdateEvent` | Updates the occupancy LED and display after the Occupancy attribute changes. |
| `SensorAttributeUpdateEventImpl` | `SensorAttributeUpdateEvent` | Updates the display after a temperature or humidity change. |
| `OnAttributeChangedImpl` | `OnAttributeChanged` | Converts Occupancy, Temperature Measurement, and Relative Humidity Measurement changes into application events. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Logs Identify attribute changes. |
