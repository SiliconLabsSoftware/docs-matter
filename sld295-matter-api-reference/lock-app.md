# Lock Application Override APIs

To override any of the following hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches the declaration in `autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback, initializes the lock, and synchronizes the Door Lock cluster state. |
| `InitLockImpl` | `InitLock` | Initializes the lock state, credential storage, actuator timers, and the Door Lock server. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Routes lock-action and function-button events. |
| `LockButtonActionHandlerImpl` | `LockButtonActionHandler` | Converts a lock-button press into a lock or unlock action. |
| `UnlatchCallbackImpl` | `UnlatchCallback` | Schedules the transition from the unlatched state to the unlocked state when the unlatch timer expires. |
| `ActuatorMovementEventHandlerImpl` | `ActuatorMovementEventHandler` | Completes the actuator movement, updates the Door Lock state, and processes any pending request. |
| `LockActionEventHandlerImpl` | `LockActionEventHandler` | Starts the lock, unlock, or unlatch action carried by an application event. |
| `LockRequestEventHandlerImpl` | `LockRequestEventHandler` | Drains a staged Door Lock request and passes it to the application task. |
| `HandleLockRequestOnAppTaskImpl` | `HandleLockRequestOnAppTask` | Queues, completes, or starts a Door Lock request according to actuator state. |
| `UnlockAfterUnlatchImpl` | `UnlockAfterUnlatch` | Changes an unlatched lock to the unlocked state and stages an unlock request. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Responds to Door Lock `LockState` attribute changes. |
| `DMDoorLockOnDoorLockCommandImpl` | `DMDoorLockOnDoorLockCommand` | Validates a Lock command and stages a request for the locked state. |
| `DMDoorLockOnDoorUnlockCommandImpl` | `DMDoorLockOnDoorUnlockCommand` | Validates an Unlock command and stages an unlock or unlatch request, depending on Unbolt support. |
| `DMDoorLockOnDoorUnboltCommandImpl` | `DMDoorLockOnDoorUnboltCommand` | Validates an Unbolt command and stages a request for the unlocked state. |
| `DMDoorLockGetCredentialImpl` | `DMDoorLockGetCredential` | Retrieves credential data for the Door Lock server. |
| `DMDoorLockSetCredentialImpl` | `DMDoorLockSetCredential` | Persists credential data for the Door Lock server. |
| `DMDoorLockGetUserImpl` | `DMDoorLockGetUser` | Retrieves user data for the Door Lock server. |
| `DMDoorLockSetUserImpl` | `DMDoorLockSetUser` | Persists user data for the Door Lock server. |
| `DMDoorLockGetWeekDayScheduleImpl` | `DMDoorLockGetWeekDaySchedule` | Retrieves a user's weekday schedule. |
| `DMDoorLockSetWeekDayScheduleImpl` | `DMDoorLockSetWeekDaySchedule` | Persists a user's weekday schedule. |
| `DMDoorLockGetYearDayScheduleImpl` | `DMDoorLockGetYearDaySchedule` | Retrieves a user's year-day schedule. |
| `DMDoorLockSetYearDayScheduleImpl` | `DMDoorLockSetYearDaySchedule` | Persists a user's year-day schedule. |
| `DMDoorLockGetHolidayScheduleImpl` | `DMDoorLockGetHolidaySchedule` | Retrieves a holiday schedule. |
| `DMDoorLockSetHolidayScheduleImpl` | `DMDoorLockSetHolidaySchedule` | Persists a holiday schedule. |
| `DMDoorLockOnAutoRelockImpl` | `DMDoorLockOnAutoRelock` | Starts a lock action when automatic relocking occurs. |
