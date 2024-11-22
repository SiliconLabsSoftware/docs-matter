# Matter API Reference

This section covers the various Application Programming Interfaces (APIs) that a developper might use when developping a new Matter Application.  

- [**DataModel**](./datamodeltypes.md)
- [**Attributes**](./attributes.md)
- [**Clusters**](./cluster.md)
- [**Commands**](./commands.md)
- [**Events**](./event.md)
- [**Cluster Implementation**](./cluster-implementation.md)

## Application APIs

### Initializaton

The application 'Init' sequence lives in the ```AppTask.cpp``` file, and is called at the beginning of the application to ensure that all components are properly initialized and ready to operate. It sets up necessary callbacks, initializes hardware components, and handles any errors that may occur during the process. This function is crucial for the stable operation of the application.

```cpp
CHIP_ERROR AppTask::Init()
```

The ```AppTask.cpp``` file may also contain event handlers and helper code useful to the application