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
2. Run `docker run -d --name some-rabbit -p 5672:5672 -p 5673:5673 -p 15672:15672 rabbitmq:3-management`
3. Set the following environmental variables:

   - PG_HOST=localhost   
   
   - PG_USER=postgres 
   
   - PG_PORT=5432 
   
   - PG_PASSWORD=password
   
4. Run `cargo test -- --nocapture`
