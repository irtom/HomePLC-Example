# HomePLC-Example

Example to demonstrate the use of all HomePLC libraries.

## Dependencies

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
