# Closure application override APIs

Override each `AppTask` hook below by declaring the `*Impl()` method in
`CustomerAppTask.h` and implementing it in `CustomerAppTask.cpp`. Match the
signature in `autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Register the button callback, initialize the display, and initialize Closure Manager. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Route closure button presses to `ClosureButtonActionEventHandler` and function button events to the base application handler. |
| `ClosureButtonActionEventHandlerImpl` | `ClosureButtonActionEventHandler` | Stop motion if a closure action is in progress, otherwise start a MoveTo toward the opposite position. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Log Identify attribute changes. |
| `DMClosureControlClusterAttributeChangedCallbackImpl` | `DMClosureControlClusterAttributeChangedCallback` | Refresh the UI when Closure Control `MainState` or `OverallCurrentState` changes. |
| `DMClosureDimensionClusterAttributeChangedCallbackImpl` | `DMClosureDimensionClusterAttributeChangedCallback` | Log Closure Dimension attribute changes. |

## ClosureManager

These APIs use the Closure app's separate manager override chain. Declare and
implement the corresponding `*Impl()` methods in `CustomerAppManager`, which
derives from `ClosureManagerImpl<CustomerAppManager>`. Use
`autogen/ClosureManagerImpl.h` for exact signatures. Do not place these
overrides in `CustomerAppTask`.

| Override | Public API | Default behavior |
|---|---|---|
| `InitImpl` | `Init` | Initialize the closure timer, closure endpoints, and panel endpoints. |
| `OnCalibrateCommandImpl` | `OnCalibrateCommand` | Validate and start an asynchronous closure calibration. |
| `OnMoveToCommandImpl` | `OnMoveToCommand` | Validate a MoveTo command and set overall panel targets. |
| `OnStopCommandImpl` | `OnStopCommand` | Stop the active closure operation and complete the stop action. |
| `OnSetTargetCommandImpl` | `OnSetTargetCommand` | Validate a SetTarget command and set the selected panel target. |
| `OnStepCommandImpl` | `OnStepCommand` | Validate a Step command and set the selected panel step target. |
| `HandleClosureActionCompleteImpl` | `HandleClosureActionComplete` | Finalize a completed calibrate, stop, move, or unlatch action. |
| `HandleClosureMotionActionImpl` | `HandleClosureMotionAction` | Advance closure panels toward their target positions. |
| `HandleClosureUnlatchActionImpl` | `HandleClosureUnlatchAction` | Update closure and panel states for an unlatch action. |
| `GetPanelNextPositionImpl` | `GetPanelNextPosition` | Calculate the next position between a panel's current and target positions. |
| `HandlePanelSetTargetActionImpl` | `HandlePanelSetTargetAction` | Advance one panel toward a SetTarget position. |
| `HandlePanelUnlatchActionImpl` | `HandlePanelUnlatchAction` | Update one panel for an unlatch action. |
| `HandlePanelStepActionImpl` | `HandlePanelStepAction` | Apply a Step action to one panel. |
