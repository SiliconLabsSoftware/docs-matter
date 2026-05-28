# Matter API Reference

This section covers the various Application Programming Interfaces (APIs) that a developer might use when developing a new Matter Application.  

- [**DataModel**](./datamodeltypes.md)
- [**Attributes**](./attributes.md)
- [**Clusters**](./cluster.md)
- [**Commands**](./commands.md)
- [**Events**](./event.md)
- [**Cluster Implementation**](./cluster-implementation.md)

## Application APIs

### Application customization models

Matter Extension 2.9.0 migrates a subset of sample apps to CRTP based architecture, which removes app manager and DataModelCallbacks files. All other sample apps keep the previous architecture until the patch release.

Check your project in Project Explorer:

| If you see… | Architecture | Where to add custom logic |
|---|---|---|
| `src/CustomerAppTask.cpp` and `autogen/AppTask.cpp` | **New** | Override `*Impl()` hooks in `CustomerAppTask`, do not edit `autogen/AppTask.cpp` |
| `src/DataModelCallbacks.cpp` and editable `src/AppTask.cpp` | **Legacy** | Callbacks in `DataModelCallbacks.cpp`, init and app logic in `src/AppTask.cpp` |

**Sample apps on the new architecture in 2.9.0:**

- Lighting (`lighting-app`)
- Zigbee Matter Light (`zigbee-matter-light`)
- On/Off Plug (`onoff-plug-app`)
- Thermostat
- Lock (`lock-app`)
- Light Switch (`light-switch-app`)
- Rangehood (`rangehood-app`)
- Platform Template (`platform-app`)
- Air Quality Sensor (`air-quality-sensor-app`)

All other Silicon Labs Matter sample apps in this release use the legacy model. Pages below label steps as **New architecture** or **Legacy architecture** where they differ.

### Initialization

**New architecture:** Default initialization lives in `autogen/AppTask.cpp`. Override `AppInitImpl()` and other `*Impl()` hooks in `src/CustomerAppTask.cpp` to customize behavior.

**Legacy architecture:** The application Init sequence lives in `src/AppTask.cpp` and is called at the beginning of the application to ensure that all components are properly initialized and ready to operate. It sets up necessary callbacks, initializes hardware components, and handles any errors that may occur during the process.

```cpp
CHIP_ERROR AppTask::Init()
```

The `AppTask.cpp` file may also contain event handlers and helper code useful to the application.
