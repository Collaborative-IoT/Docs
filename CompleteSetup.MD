# Complete Setup one file
In order to setup the Collaborative-IoT system you need to setup one ControlServer(Merlin), one rabbitmq instance, one integration server(Bors), the frontend
interface(Hector) and one postgres instance.

# Merlin(control server) Setup

## Env variables needed 
```
PG_HOST -> postgres host
PG_USER -> postgres user
PG_PORT -> postgres port
PG_PASSWORD -> postgres password
DC_CLIENT_ID -> Discord Client ID for oauth
GH_CLIENT_ID -> Github Client ID for oauth
BASE_UI_URL -> The location of the frontend interface(example:http://127.0.0.1:3000).
MERLIN_LOCATION-> The location/address of the server without specific protocols noted(example `127.0.0.1:50888`).
MERLIN_TLS_OR_NOT -> Use tls?(it should be `y` or `n`).
MERLIN_TLS_CERT -> TLS CERT(cert.pem) only applies if using tls
MERLIN_TLS_KEY -> TLS KEY(key.rsa) only applies if using tls
BASE_API_URL -> The location of the merlin api itself(formatted like http or https://{MERLIN_LOCATION} merlin_location could be 127.0.0.1:50888).
```

## Step by step to start the server
1. Clone the repo(`https://github.com/Collaborative-IoT/Merlin`)
2. Make sure you have the env variables set above.
3. Make sure you have Rust/Cargo installed on your local machine https://www.rust-lang.org/
4. Run `cargo install`, `cargo run`.

# Bors(integration server) Setup
There are no env variables needed or config since it 

## Step by step
1. Clone the repo(`https://github.com/Collaborative-IoT/Bors`)
2. Make sure you have Rust/Cargo installed on your local machine https://www.rust-lang.org/
3. Run `cargo install`, `cargo run`.

# RabbitMQ setup
Make sure you spawn a default rabbitmq instance on the default 15672 port with the guest/guest user-password.

# Hector(web interface)

## Env variables needed
```
NEXT_PUBLIC_API_BASE_URL -> The http location of Merlin(with the http:// in the string ex:http://127.0.0.1:3030)
NEXT_PUBLIC_BASE_URL -> The hosted location of the web interface(with the http:// in the string ex:http://127.0.0.1:3000)
NEXT_PUBLIC_WS_API_URL -> The ws location of merlin(with the wss or ws included in the string ex:ws://127.0.0.1:3030/user-api)
```

## Step by step
This is a normal next.js application and there isn't any weird stuff needed to start it.
Just follow the normal react/next.js starting procedure.

# Lancelot
This is a normal node application that shouldn't require any weird stuff to start it. 
Just follow the normal node procedure to start it.
You will need the packages needed to support mediasoup natively though, so please check the mediasoup documentation and follow the setup.
