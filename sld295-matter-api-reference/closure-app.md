# Closure Application Override APIs

To override any of the following AppTask hooks, declare the corresponding `*Impl()` method in `CustomerAppTask.h` and implement it in `CustomerAppTask.cpp`. Ensure that the method signature matches the declaration in `autogen/AppTaskImpl.h`.

## AppTask

| Override | Public API | Default behavior |
|---|---|---|
| `AppInitImpl` | `AppInit` | Registers the button callback, initializes the display, and initializes Closure Manager. |
| `ButtonEventHandlerImpl` | `ButtonEventHandler` | Routes closure button presses to `ClosureButtonActionEventHandler` and function button events to the base application handler. |
| `ClosureButtonActionEventHandlerImpl` | `ClosureButtonActionEventHandler` | Stops motion if a closure action is in progress; otherwise, it starts a MoveTo toward the opposite position. |
| `DMPostAttributeChangeCallbackImpl` | `DMPostAttributeChangeCallback` | Logs Identify attribute changes. |
| `DMClosureControlClusterAttributeChangedCallbackImpl` | `DMClosureControlClusterAttributeChangedCallback` | Refreshes the UI when Closure Control `MainState` or `OverallCurrentState` changes. |
| `DMClosureDimensionClusterAttributeChangedCallbackImpl` | `DMClosureDimensionClusterAttributeChangedCallback` | Logs Closure Dimension attribute changes. |

## ClosureManager

These APIs use the Closure app's separate manager override chain. Declare and
implement the corresponding `*Impl()` methods in `CustomerAppManager`, which
derives from `ClosureManagerImpl<CustomerAppManager>`. Use
`autogen/ClosureManagerImpl.h` for exact signatures. Do not place these
overrides in `CustomerAppTask`.

| Override | Public API | Default behavior |
|---|---|---|
| `InitImpl` | `Init` | Initializes the closure timer, closure endpoints, and panel endpoints. |
| `OnCalibrateCommandImpl` | `OnCalibrateCommand` | Validates and starts an asynchronous closure calibration. |
| `OnMoveToCommandImpl` | `OnMoveToCommand` | Validates a MoveTo command and sets overall panel targets. |
| `OnStopCommandImpl` | `OnStopCommand` | Stops the active closure operation and completes the stop action. |
| `OnSetTargetCommandImpl` | `OnSetTargetCommand` | Validates a SetTarget command and sets the selected panel target. |
| `OnStepCommandImpl` | `OnStepCommand` | Validates a Step command and sets the selected panel step target. |
| `HandleClosureActionCompleteImpl` | `HandleClosureActionComplete` | Finalizes a completed calibrate, stop, move, or unlatch action. |
| `HandleClosureMotionActionImpl` | `HandleClosureMotionAction` | Advances closure panels toward their target positions. |
| `HandleClosureUnlatchActionImpl` | `HandleClosureUnlatchAction` | Updates closure and panel states for an unlatch action. |
| `GetPanelNextPositionImpl` | `GetPanelNextPosition` | Calculates the next position between a panel's current and target positions. |
| `HandlePanelSetTargetActionImpl` | `HandlePanelSetTargetAction` | Advances one panel toward a SetTarget position. |
| `HandlePanelUnlatchActionImpl` | `HandlePanelUnlatchAction` | Updates one panel for an unlatch action. |
| `HandlePanelStepActionImpl` | `HandlePanelStepAction` | Applies a Step action to one panel. |
