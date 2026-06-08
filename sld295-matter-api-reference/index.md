# Matter API Reference

This section covers the various Application Programming Interfaces (APIs) that a developer might use when developing a new Matter Application.  

- [**DataModel**](./datamodeltypes.md)
- [**Attributes**](./attributes.md)
- [**Clusters**](./cluster.md)
- [**Commands**](./commands.md)
- [**Events**](./event.md)
- [**Cluster Implementation**](./cluster-implementation.md)

## Application APIs

### Application Customization Models

Matter Extension 2.9.0 migrates a subset of sample apps to the Curiously Recurring Template Pattern (CRTP) based architecture, which removes app manager and DataModelCallbacks files. All other sample apps keep the previous architecture until the patch release.

Check your project in Project Explorer:

| If you see… | Architecture | Where to add custom logic |
|---|---|---|
| `src/CustomerAppTask.cpp` and `autogen/AppTask.cpp` | **New** | Override `*Impl()` hooks in `CustomerAppTask`, do not edit `autogen/AppTask.cpp` |
| `src/DataModelCallbacks.cpp` and editable `src/AppTask.cpp` | **Legacy** | Callbacks in `DataModelCallbacks.cpp`, init and app logic in `src/AppTask.cpp` |

**Sample apps on the new architecture in 2.9.0:**

- Lighting 
- Zigbee Matter Light
- On/Off Plug
- Thermostat
- Lock
- Light Switch
- Rangehood
- Platform Template
- Air Quality Sensor

All other Silicon Labs Matter sample apps in this release use the legacy model. Pages below label steps as **New architecture** or **Legacy architecture** where they differ.

### Initialization

**New architecture:** Default initialization is included in `autogen/AppTask.cpp`. Override `AppInitImpl()` and other `*Impl()` hooks in `src/CustomerAppTask.cpp` to customize behavior.

**Legacy architecture:** The application Init sequence is included in `src/AppTask.cpp` and is called at the beginning of the application to ensure that all components are properly initialized and ready to operate. It sets up necessary callbacks, initializes hardware components, and handles any errors that may occur during the process.

```cpp
CHIP_ERROR AppTask::Init()
```

The `AppTask.cpp` file may also contain event handlers and helper code useful to the application.
