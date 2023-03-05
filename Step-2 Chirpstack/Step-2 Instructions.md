# **Overview**

One of the benefits of the RAK developer gateway used for this project is that it comes pre-installed with Chirpstack, you can refer back to the [Step-1 Instructions](https://github.com/adamschreck/pea-pod/blob/main/Step-1%20Gateway%20and%20Computer%20Setup/Step-1%20Instructions.md#setup-rak-gateway-channel-plan) to see where you enabled Chirpstack. Within the pea-PODs architecture Chirpstack serves the purpose of both the network server and the application server. Refer back to this [diagram](https://github.com/adamschreck/pea-pod#diagram-describing-pea-pod-architecture) for more context on what that means. In addition the pea-POD leverages an integration created by Chirpstack to store data collected in a PostgreSQL server. This will allow for easy access and retrieval of the data. The below steps will explain how to login to Chirpstack, which if you have completed the ***Step-1 Instructions*** is already runnning on your Pi. Additionally, this will pull in formation directly from the [original POD build guide](https://github.com/oats-center/pod/blob/main/build-guide.md) regarding how to get started with Chirpstack. After this, other content has been sourced from [Chirpstack's guide to setting up the PostgrsSQL integration](https://www.chirpstack.io/application-server/integrations/postgresql/). 

# **Steps**

## Login to Chirpstack

Chirpstack can be accessed in one of two ways:
- If you are connected to the same internet as the Pi, then visit `your Pi's IP address:8080` in your browser. The 8080 refers to what is known as the "port number", which identifies where that program is running on the device.
  - For example: `10.0.0.145:8080`

 In this case it is saying that the Chirpstack program is running on port `8080` of the Pi called `10.0.0.145`.

- If you use Cloudflare tunnels, detailed in `Step-5 Instructions`, then you can visit your Chripstack tunnel URL.
  - For example: `pea-pod-adam-cs.oatscenter.org`

## Setup your Chirpstack

### Change the default login

The default username and password is: `admin / admin`. It is recommended that you at least change the password, particularly if you are using Cloudflare tunnels.
This can be done by clicking the word `admin` in the top right corner of the screen and choosing `change password`.
You may change it to whatever you want, but don't forget it!

![Screen Shot 2023-03-04 at 2 50 40 PM](https://user-images.githubusercontent.com/126691160/222926003-13bd44a7-469f-49a8-9a9a-43f37a55007b.png)

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

## Enable Integration

The PostgreSQL integration writes all device related events logged in Chirpstack into a PostgreSQL database. This allows your device data to be queried or used by other applications. Specifically in the instance of the pea-POD, so that it can be visualized using Grafana.

Within Chirpstack, once you have set up a device such as a sensor, it is possible to view device data. Additionally, Chirpstack natively stores this device data in a PostgresSQL server. However, data stored in that database is only kept temporarily. To overcome this, the PostgresSQL integration can be enabled. If the integration is enabled, it will automatically create all database tables on startup. It is important that this integration uses its own database, to avoid schema collisions.

### Create the database

Please see below an example for creating the PostgreSQL database. Depending your PostgreSQL installation, these commands might be different.

1. Begin from your Terminal command line and logged into your PI.

2. Enter the PostgreSQL as the postgres user:

    sudo -u postgres psql

***Within the PostgreSQL prompt, enter the following queries:***

3. Create the chirpstack_as_events user

    create role chirpstack_as_events with login password 'dbpassword';

4. Create the chirpstack_as_events database

    create database chirpstack_as_events with owner chirpstack_as_events;

5. Enable the hstore extension

    \c chirpstack_as_events
    create extension hstore;

6. Exit the prompt

    \q

7. To verify if the user and database have been setup correctly, try to connect to it:

    psql -h localhost -U chirpstack_as_events -W chirpstack_as_events

### Activate the integration***

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