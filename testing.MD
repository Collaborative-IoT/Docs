# Testing

There are both integration tests and unit tests for the complete platform. The integration tests are targeted at ensuring server state is altered correctly
communication is effective. The unit tests are simple and test each testable individual unit of the system.


# Testing Merlin
 
## Merlin Tests Explained

Merlin requires there to be a RabbitMQ instance running, because it tests the modules against things like room creation and other things that requires messages to be published to the queues. For example, when a room is triggered for creation a message is sent to the voice server via rabbitmq, so we make sure the modules are pushing the correct data in the different cases.

Merlin requires a PostgresSQL instance to be running during the tests, we test our data capture modules to make sure they are correct. Please note that every single test will require a fresh empty copy of the database. We plan to add a cleanup after every test.

Merlin is a Cargo project, so you will need to have Rust/Cargo completely configured on your local machine to run the tests, using `cargo test` should test all of the individual cases from Merlin's scope.

## Steps to setting running these tests(docker)
We will only be using docker to spin up quick rabbitmq and postgres instances without hassle. Merlin itself will need to be ran using cargo. Please note that the env variables below for postgres can be modified as need be, this is just the way I do things.

1. Run `docker run --name pg3 -p  5432:5432  -e POSTGRES_PASSWORD=password postgres`
2. Run `docker run --name some-rabbit -p 5672:5672 -p 5673:5673 -p 15672:15672 rabbitmq:3-management`
3. Set the following environmental variables:

   - PG_HOST=localhost   
   
   - PG_USER=postgres 
   
   - PG_PORT=5432 
   
   - PG_PASSWORD=password
   
4. Run `cargo test -- --nocapture`


## Merlin Tests in Depth

Merlin has a core module called communication_handler, which handles the overarching logic for requests like making sure you aren't making
easily detected illegal requests. Whenever makes an illegal request we respond to their websocket connection and with an error.
Merlin is async so this means we are using a task based system, each user has an executing task that handles its websocket message sending.
We send messages to these tasks by using Multi Producer Single Consumer channels and this is how we essentially test whether or not the response messages are correct or not. Normally we would create a channel and then link the channel to the websocket task, but in the tests we skip the websocket part and just consume the messages and assert after we know one should have been sent.

The same thing is true for checking if messages to the voice server(via rabbitmq) are correct or not. We publish and then read from a channel after executing a communication handler function to make sure the contents are correct for the request we made.

## Merlin Tests Mock-Users vs Real-Users

In the code you will come across the concept of mock-users vs real-users. Mock users are users without an associated user row, but they exist in a server state, real users have this associated user row. This is important because some requests/communication handler functionality checks the database for user data and assumes that it is there. So for example, searching for user previews of a specific room will grab all users of a room and search the database for their avatar url/display name. If a mock user is in a room when this preview search happens, we will run into an out of bounds panic, so only real users must be in the room for these sort of requests. So you will see user "33" being removed and added back sometimes due to their status of a mock-user.


