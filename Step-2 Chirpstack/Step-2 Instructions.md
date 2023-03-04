# **Overview**

One of the benefits of the RAK developer gateway used for this project is that it comes pre-installed with Chirpstack, you can refer back to the [Step-1 Instructions](https://github.com/adamschreck/pea-pod/blob/main/Step-1%20Gateway%20and%20Computer%20Setup/Step-1%20Instructions.md#setup-rak-gateway-channel-plan) to see where you enabled Chirpstack. Within the pea-PODs architecture Chirpstack serves the purpose of both the network server and the application server. Refer back to this [diagram](https://github.com/adamschreck/pea-pod#diagram-describing-pea-pod-architecture) for more context on what that means. In addition the pea-POD leverages an integration created by Chirpstack to store data collected in a PostgreSQL server. This will allow for easy access and retrieval of the data. The below steps will explain how to login to Chirpstack, which if you have completed the ***Step-1 Instructions*** is already runnning on your Pi. Additionally, this will pull in formation directly from the [original POD build guide](https://github.com/oats-center/pod/blob/main/build-guide.md) regarding how to get started with Chirpstack. After this, other content has been sourced from [Chirpstack's guide to setting up the PostgrsSQL integration](https://www.chirpstack.io/application-server/integrations/postgresql/). 

# **Steps**

## Login to Chirpstack

Chirpstack can be accessed in one of two ways:
- If you are connected to the same home internet as the Pi, then visit `your router's IP address:8080` in your browser.

- If you use Cloudflare tunnels, detailed in `Step-5 Instructions`then you can visit your Chripstack tunnel URL.
  - For example, `pea-pod-adam-cs.oatscenter.org`

## Setup your Chirpstack

### Change the default login

The default username and password is: `admin / admin`.
We recommend that you at least change the password, particularly if you are using Cloudflare tunnels.
This can be done by clicking the word `admin` in the top right corner of the screen and choosing `change password`.
You may change it to whatever you want, but don't forget it!

### Adding the physical gateway

Select `Gateways` from the left menu panel under `Tenant`, and choose `Add gateway`.
Use these settings:

- Gateway name: Something that uniquely identifies the gateway. For our RAK 7289 we used `RAK7289C_4D65`.
- Gateway description: We used `RAK7289 Gateway attached to POD`
- Gateway ID: Your gateway manual should describe how to locate this.
- Choose `Submit`.

After a few minutes, refresh the "Gateways" page until the `Last seen` column as a time or `a few seconds ago` rather than `Never`.
### Create your POD application

Applications in Chirpstack hold a set of devices to communicate with.
They also control how the received device data is set to integrated systems, like Thingsboard.

To create an application, go to Applications from the left panel menu, and select `+ CREATE`.
Please use these settings:

- Application name: `POD-Kit`
- Application description: `POD Kit Sensors`
- Service-profile: `POD Profile`

Select `CREATE APPLCATION`

Add Thingsboard integration
- Go to the Integrations tab within `POD-Kit`
- Under Thingsboard.io click `ADD`
- For the thingsboard.io server use `http://thingsboard:9090`
- Click `Update Integration` 

## Enable Integration
PostgreSQL
The PostgreSQL integration writes all device related events into a PostgreSQL database, so that it can be queried by other applications or so that it can be visualized using for example Grafana using the PostgreSQL Data Source.

If the integration is enabled, it will automatically create all database tables on startup. It is important that this integration uses its own database, to avoid schema collisions.

Create the database
Please see below an example for creating the PostgreSQL database. Depending your PostgreSQL installation, these commands might be different.

Enter the PostgreSQL as the postgres user:

    sudo -u postgres psql

Within the PostgreSQL prompt, enter the following queries:


-- create the chirpstack_as_events user
    create role chirpstack_as_events with login password 'dbpassword';

-- create the chirpstack_as_events database
    create database chirpstack_as_events with owner chirpstack_as_events;

-- enable the hstore extension
    \c chirpstack_as_events
    create extension hstore;

-- exit the prompt
    \q
To verify if the user and database have been setup correctly, try to connect to it:

    psql -h localhost -U chirpstack_as_events -W chirpstack_as_events

Activating the integration

In order for ChirpStack to start writing event data to a Postgres database, the integration must be explicitly enabled and configured in the `chirpstack-application-server.toml` configuration file.

Enabling the integration
In the file, find this section:


    [application_server.integration]

Enabled integrations.

    enabled=["mqtt"]

Your enabled line may look slightly different, as you may have other integrations already active. Add "postgresql" to the array. In this case, the modified line should appear as enabled=["mqtt", "postgresql"].

Integration configuration
You must also set the configuration settings for the integration. If your configuration file does not already contain the following section, add it now:

    [application_server.integration.postgresql]
    dsn="postgres://<username>:<password>@<host>/<database>?sslmode=disable"

In the dns= line, modify <username>, <password>, <host>, and <database> with your appropriate credentials and targets. If you followed the example above, you would use chirpstack_as_events as your username and target database. If your target Postgres database is on the same machine as the Application Server, use localhost as your host.

Please see Configuration for a full configuration example.