# Matter API Reference

This section covers the various Application Programming Interfaces (APIs) that a developer might use when developing a new Matter Application.  

- [**DataModel**](./datamodeltypes.md)
- [**Attributes**](./attributes.md)
- [**Clusters**](./cluster.md)
- [**Commands**](./commands.md)
- [**Events**](./event.md)
- [**Cluster Implementation**](./cluster-implementation.md)

## Application APIs

For information about customizing app behavior with `CustomerAppTask`, see [Extending Base App Implementation](/matter/{build-docspace-version}/matter-references/custom-matter-device/#extending-base-app-implementation).

### Initialization

Default initialization is included in `autogen/AppTask.cpp`. Override `AppInitImpl()` and other `*Impl()` hooks in `src/CustomerAppTask.cpp` to customize behavior.

```cpp
CHIP_ERROR AppTask::Init()
```

The `AppTask.cpp` file may also contain event handlers and helper code useful to the application.
