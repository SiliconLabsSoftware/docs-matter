# Lock application override APIs

Override each hook below by declaring the `*Impl()` method in `CustomerAppTask.h`
and implementing it in `CustomerAppTask.cpp`. Match the signature in
`autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Register the button callback, initialize the lock, and sync the Door Lock cluster state. |
| `InitLockImpl` | `InitLock` | Initialize lock state, credential storage, actuator timers, and the Door Lock server. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Route lock action and function button events. |
| `LockButtonActionHandlerImpl` | `LockButtonActionHandler` | Convert a lock button press into a lock or unlock action. |
| `UnlatchCallbackImpl` | `UnlatchCallback` | Schedule the transition from the unlatched state to the unlocked state when the unlatch timer expires. |
| `ActuatorMovementEventHandlerImpl` | `ActuatorMovementEventHandler` | Complete actuator motion, update the Door Lock state, and process a pending request. |
| `LockActionEventHandlerImpl` | `LockActionEventHandler` | Start the lock, unlock, or unlatch action carried by an application event. |
| `LockRequestEventHandlerImpl` | `LockRequestEventHandler` | Drain a staged Door Lock request and pass it to the application task. |
| `HandleLockRequestOnAppTaskImpl` | `HandleLockRequestOnAppTask` | Queue, complete, or start a Door Lock request according to actuator state. |
| `UnlockAfterUnlatchImpl` | `UnlockAfterUnlatch` | Change an unlatched lock to unlocked and stage the unlock request. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Respond to Door Lock `LockState` attribute changes. |
| `DMDoorLockOnDoorLockCommandImpl` | `DMDoorLockOnDoorLockCommand` | Validate a Lock command and stage a request for the locked state. |
| `DMDoorLockOnDoorUnlockCommandImpl` | `DMDoorLockOnDoorUnlockCommand` | Validate an Unlock command and stage an unlock or unlatch request, depending on Unbolt support. |
| `DMDoorLockOnDoorUnboltCommandImpl` | `DMDoorLockOnDoorUnboltCommand` | Validate an Unbolt command and stage a request for the unlocked state. |
| `DMDoorLockGetCredentialImpl` | `DMDoorLockGetCredential` | Retrieve credential data for the Door Lock server. |
| `DMDoorLockSetCredentialImpl` | `DMDoorLockSetCredential` | Persist credential data for the Door Lock server. |
| `DMDoorLockGetUserImpl` | `DMDoorLockGetUser` | Retrieve user data for the Door Lock server. |
| `DMDoorLockSetUserImpl` | `DMDoorLockSetUser` | Persist user data for the Door Lock server. |
| `DMDoorLockGetWeekDayScheduleImpl` | `DMDoorLockGetWeekDaySchedule` | Retrieve a user's weekday schedule. |
| `DMDoorLockSetWeekDayScheduleImpl` | `DMDoorLockSetWeekDaySchedule` | Persist a user's weekday schedule. |
| `DMDoorLockGetYearDayScheduleImpl` | `DMDoorLockGetYearDaySchedule` | Retrieve a user's year day schedule. |
| `DMDoorLockSetYearDayScheduleImpl` | `DMDoorLockSetYearDaySchedule` | Persist a user's year day schedule. |
| `DMDoorLockGetHolidayScheduleImpl` | `DMDoorLockGetHolidaySchedule` | Retrieve a holiday schedule. |
| `DMDoorLockSetHolidayScheduleImpl` | `DMDoorLockSetHolidaySchedule` | Persist a holiday schedule. |
| `DMDoorLockOnAutoRelockImpl` | `DMDoorLockOnAutoRelock` | Start a lock action when automatic relocking occurs. |
