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


