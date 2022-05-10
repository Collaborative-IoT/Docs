# Bors
Bors is the integration server, take a look at the design portion of the documentation to learn more.

## House Of IoT integration.
The HOI integration is something special due to the limitation of action execution by one specific client enforced by the design of the HOI server.
Only one action/passive data gather can run at a specific time, so this means that we had to implement a queue for actions to comply with the design.

The client integration follows the server documentation down to the deepest detail. If you want to learn more about this Iot server you can check the [docs](https://github.com/House-of-IoT).
