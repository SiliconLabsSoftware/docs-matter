# Multi Sensor application override APIs

Override each hook below by declaring the `*Impl()` method in `CustomerAppTask.h`
and implementing it in `CustomerAppTask.cpp`. Match the signature in
`autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Register the button callback, initialize the occupancy LED and display, and start the sensor manager. |
| `InitSensorManagerImpl` | `InitSensorManager` | Initialize sensor clusters, register the attribute listener, and schedule periodic sampling. |
| `GetTemperatureAndHumidityImpl` | `GetTemperatureAndHumidity` | Read the Si70xx sensor when present, otherwise supply simulated temperature and humidity values. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Route function button events and occupancy toggle button events. |
| `ProcessButtonEventImpl` | `ProcessButtonEvent` | Toggle the Occupancy attribute for an application button event. |
| `TriggerSensorActionImpl` | `TriggerSensorAction` | Sample temperature and humidity and update their measured value attributes. |
| `OccupancyAttributeUpdateEventImpl` | `OccupancyAttributeUpdateEvent` | Update the occupancy LED and display after an Occupancy change. |
| `SensorAttributeUpdateEventImpl` | `SensorAttributeUpdateEvent` | Update the display after a temperature or humidity change. |
| `OnAttributeChangedImpl` | `OnAttributeChanged` | Translate Occupancy, Temperature Measurement, and Relative Humidity Measurement changes into application events. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Log Identify attribute changes. |
