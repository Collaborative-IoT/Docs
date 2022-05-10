# Bors
Bors is the integration server, take a look at the design portion of the documentation to learn more.

## House Of IoT integration.
The HOI integration is something special due to the limitation of action execution by one specific client enforced by the design of the HOI server.
Only one action/passive data gather can run at a specific time, so this means that we had to implement a queue for actions to comply with the design.

Every time we want to execute an action, the action is queued up and we wait until no actions are executing to start a new "action cycle". Each action cycle starts with the action message from the [control server](https://github.com/Collaborative-IoT/Merlin), and it ends with a single response from the HOI server.

This is a very simple rule we use to avoid confusion when executing actions.

![action_cycle_diagram](https://user-images.githubusercontent.com/35206353/167528408-cf525c0e-1c65-4831-9e8b-2537c9ad0b53.png)


The client integration follows the server documentation down to the deepest detail. If you want to learn more about this Iot server you can check the [docs](https://github.com/House-of-IoT).
