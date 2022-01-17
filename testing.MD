# Testing

There are both integration tests and unit tests for the complete platform. The integration tests are targeted at ensuring server state is altered correctly
communication is effective. The unit tests are simple and test each testable individual unit of the system.


## Testing Merlin(GeneralControlServer) and Arthur(API-Client)

Merlin requires there to be a PostgresSQL and RabbitMQ instance running(find more details taking a look at the setup documentation).
Merlin is a Cargo project, so you will need to have Rust/Cargo completely configured on your local machine to run the tests, using `cargo test` should test
all individual unit tests.

To run the integration tests, you will need to start the server and then run both of the two test clients(find more details taking a look at the setup documentation).
The idea of the integration tests is to ensure that the server and the client is working correctly by asserting the responses in order.

It is important to always have a fresh instance of Postgres running for every test(easy to just spin up a docker container and avoid persisting data using volumes, then cleaning the leftover data).

# Cheat Sheet

Running the postgres instance with no specific volume: `sudo docker run --name pg3 -p  5432:5432  -e POSTGRES_PASSWORD=password postgres`
Running the rabbitmq instance `docker run -d --name some-rabbit -p 5672:5672 -p 5673:5673 -p 15672:15672 rabbitmq:3-management`
