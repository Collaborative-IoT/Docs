# Setup

There are multiple different versions of the GeneralControlServer(Merlin) that you run, each of them require differen't
environmental variables to run the service smoothly. To spare confusion we will list them all and what they are for.

# Environmental Variables

Postgres:
  - PG_HOST - Host for your postgres database instance.
  - PG_USER - User for your postgres database instance.
  - PG_PORT - Port for your postgres database instance.
  - PG_PASSWORD - Password for your postgres database instance.

Other:
  - DC_CLIENT_ID - Discord ClientID for oauth.
  - BASE_API_URL - The base api url for your server instace, for example http://localhost:3000 or what is used for production,
    this is used strictly for generating callback urls etc.
  - GH_CLIENT_ID - Github ClientID for oauth.
  - DC_CLIENT_SECRET - Discord client secret for oauth.
  - GH_CLIENT_SECRET - Github client secret for oauth.
  - GENERAL_HOST - Host for your server.
  - GENERAL_PORT - Port for your server.


