# The Design of Collaborative

Collaborative has a few different parts that make up the full platform:
-  [ControlServer](https://github.com/Collaborative-IoT/GeneralControlServer)
-  Interfaces([Web](https://github.com/Collaborative-IoT/Web-Frontend), [Desktop](https://github.com/Collaborative-IoT/Desktop-App), [Mobile](https://github.com/Collaborative-IoT/Mobile-App))
-  [VoiceServer](https://github.com/Collaborative-IoT/VoiceServer)
-  Postgres


## How does communication work?
Users can create "Rooms" and these rooms are the construct for all communication. Everyone in a specific room has their voice broadcasted to everyone else
same with text chat.

# How does communication work with IoT servers?
The control server will gather a request  from a moderator in a room to open a connection to a specific type 
of IoT server, the control server will connect to this IoT server and begin communication.

Each IoT server connected to by the ControlServer must have a way to broadcast "actions" for the devices currently connected. Actions
are the functionality of dead smart device connected to the IoT server. Without knowing what devices can do, the server can't make 
control requests to control the devices on behalf of the users.


For example, House-Of-Iot sends a list of actions that each device can execute in its passive data responses. These actions are then sent to the frontend
and users in a specific room can see what each device can do. They can press a button on the UI which will send a request to the ControlServer which will
trigger a request to the IoT Server.

# Why not just connect directly to the IoT Server and Ignore Collaborative?
Collaborative makes giving access to your IoT server easy and secure, since one doesn't have to directly give their authentication credentials to someone
in order for them to demo or mess with their IoT server instance. You also get built in collaboration with other active users which is interesting for building a community around IoT.


# Responsibilty of all services?
ControlServer:
- Handles authentication
- Gives credentials to connect to the voice server
- Handles chat
- Handles all communication with the database
- Handles all user requests

VoiceServer:
- Handles voice chat
- Gives credentials to ControlServer for new voice connections

RabbitMq:
- Broker messages between ControlServer and VoiceServer
