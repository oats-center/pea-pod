# **Overview**

Within the pea-PODs architecture Chirpstack serves the purpose of 

# **Steps**

## Login to Chirpstack



## Chirpstack configuration

Chirpstack can be accessed in one of two ways:

- If you are connected to the POD Wi-Fi, then visit `10.60.0.1:8080` in your browser.
- If you use Cloudflare tunnels, then visit your Chripstack tunnel URL.
  - For example, `pod-acre-welch-cs.oatscenter.org`

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