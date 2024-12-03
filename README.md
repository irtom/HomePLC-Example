# HomePLC-Example

Example to demonstrate the use of all HomePLC libraries.

## Dependencies

Download and install the latest releases of the following libraries before opening this solution:

- [HomePLC AlarmManager](https://github.com/irtom/HomePLC-AlarmManager)
- [HomePLC DIO](https://github.com/irtom/HomePLC-DIO)
- [HomePLC Home](https://github.com/irtom/HomePLC-Home)
- [HomePLC LinkManager](https://github.com/irtom/HomePLC-LinkManager)
- [HomePLC Logging](https://github.com/irtom/HomePLC-Logging)

## Contents

This repository shows how to use the HomePLC libraries to set up a custom home with buttons, lights, sockets, indicator lights and an alarm.
The intention is to create a robust backbone based on a Beckhoff PLC. On top of this further automation can be added such as Home Assistant. If Home Assistant fails, all buttons, lights, sockets, etc will still work.
Also included in the example:

- creating different floors, areas, wall plate definitions for a structured home
- all-off functionality on long press of any button

Using the libraries it is now easy to define the link between inputs and outputs as shown in the example code below:

```
// First floor - entrance spot lights
ILinkManager.Link.InputGroup.AddInput(IO.FirstFloor.Entrance.wpDoor.fbButton4);
ILinkManager.Link.InputGroup.AddInput(IO.FirstFloor.Entrance.wpStairs.fbButton3);
ILinkManager.Link.InputGroup.AddInput(IO.FirstFloor.StorageRoom.wpRoom.fbButton1);
ILinkManager.Link.OutputReaction.OnShortPress := E_DOCommand.Toggle;
ILinkManager.Link.OutputGroup.AddOutput(IO.FirstFloor.Entrance.fbSpotLights);
ILinkManager.Link.OutputGroup.AddIndicator(IO.FirstFloor.Entrance.wpDoor.fbLed4);
ILinkManager.CommitLink();
```

First different buttons are added to the input group. If one of these buttons is short pressed, the output group will toggle its state. In the output group only one output is added along with an indicator. The indicator is also an output which is used to show the status of the outputs in the group. In this case an LED on the wall plate is used. The link is finally committed and a new definition can follow.

In practice this will do the following:
- Any button from the input group is short pressed: the output toggles along with the indicator (from off to on or from on to off)
- Any button from the input group is long/double pressed: nothing happens because it was not defined what should happen in these cases
- The output fbSpotLights is manipulated externally (e.g. by Home Assistant): the indicator follows the state of the output
