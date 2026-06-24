# Matter API Reference

This section covers the various Application Programming Interfaces (APIs) that a developer might use when developing a new Matter Application.  

- [**DataModel**](./datamodeltypes.md)
- [**Attributes**](./attributes.md)
- [**Clusters**](./cluster.md)
- [**Commands**](./commands.md)
- [**Events**](./event.md)
- [**Cluster Implementation**](./cluster-implementation.md)

## Application APIs

For guidance on new vs legacy sample app architecture and where to add custom logic, see [Application Customization Models](/matter/{build-docspace-version}/matter-references/custom-matter-device/#application-customization-models).

### Initialization

**New architecture:** Default initialization is included in `autogen/AppTask.cpp`. Override `AppInitImpl()` and other `*Impl()` hooks in `src/CustomerAppTask.cpp` to customize behavior.

**Legacy architecture:** The application Init sequence is included in `src/AppTask.cpp` and is called at the beginning of the application to ensure that all components are properly initialized and ready to operate. It sets up necessary callbacks, initializes hardware components, and handles any errors that may occur during the process.

```cpp
CHIP_ERROR AppTask::Init()
```

The `AppTask.cpp` file may also contain event handlers and helper code useful to the application.
