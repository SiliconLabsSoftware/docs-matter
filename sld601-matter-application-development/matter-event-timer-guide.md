
# Event and timer (Matter)

# Event handler

The Matter event handler uses the FreeRTOS queue to transport a message from the producer to the consumer area. Events can be used to create an asynchronous message processing or an inter-task message communication.

Steps to make the event work:

- Make sure the queue is initialize
- Create an AppEventType for your application
- Populate the Type and Handler variable
- Post the message to the queue

## Event definition enum

__AppEvent__ contains event types and event structures that are used for specific applications, if needed. __Handler__ is used to store the callback for the event.

```C
struct AppEvent
{
    enum AppEventTypes
    {
        kEventType_Button = 0,
        kEventType_Timer,
        kEventType_Light,
        kEventType_Install,
        kEventType_Observer,
    };

    uint16_t Type;

    union
    {
        struct
        {
            uint8_t Action;
        } ButtonEvent;
        struct
        {
            void * Context;
        } TimerEvent;
        struct
        {
            uint8_t Action;
            int32_t Actor;
        } LightEvent;
    };

    EventHandler Handler;
};
```

## Queue posting

Creating an event and push it to the event queue. For that event to work, we need a minimum, __Handler__ and __Type___ to be defined.

```C
void AppTask::CreateObserverEvent(void)
{
    AppEvent active_mode_event = {};
    active_mode_event.Type     = AppEvent::kEventType_Observer;
    active_mode_event.Handler  = SilabsSensors::SendSensorsValues;

    sAppTask.PostEvent(&active_mode_event);
}
```

## Callback

Observer event callback

```C
void SilabsSensors::SendSensorsValues(AppEvent * aEvent)
{
    // Do something
}
```

## Dispatcher

__AppTaskMain__ is dispatching all the events from the event list.

```C
void AppTask::AppTaskMain(void * pvParameter)
{
    AppEvent event;
    QueueHandle_t sAppEventQueue = *(static_cast<QueueHandle_t *>(pvParameter));

    CHIP_ERROR err = sAppTask.Init();
    if (err != CHIP_NO_ERROR)
    {
        SILABS_LOG("AppTask.Init() failed");
        appError(err);
    }

#if !(defined(CHIP_CONFIG_ENABLE_ICD_SERVER) && CHIP_CONFIG_ENABLE_ICD_SERVER)
    sAppTask.StartStatusLEDTimer();
#endif

    sAppTask.RegisterObserver();

    SILABS_LOG("App Task started");

    while (true)
    {
        BaseType_t eventReceived = xQueueReceive(sAppEventQueue, &event, portMAX_DELAY);
        while (eventReceived == pdTRUE)
        {
            sAppTask.DispatchEvent(&event);
            eventReceived = xQueueReceive(sAppEventQueue, &event, 0);
        }
    }
}
```

# Matter Timer

## Start

Enable a one shot timer to trigger in 10 seconds with __TestCallback__ as a callback.

```C
System::Clock::Timeout Timeout = System::Clock::Seconds32(10);

chip::DeviceLayer::PlatformMgr().LockChipStack();
err = DeviceLayer::SystemLayer().StartTimer(Timeout, TestCallback, this);
chip::DeviceLayer::PlatformMgr().UnlockChipStack();
```

## Callback

Timer callback

```C
void AppTask::TestCallback(System::Layer * layer, void * aAppState)
{
	// Do something
}
```

If you need a periodic timer, you can recall __StarTimer()__ in the callback.