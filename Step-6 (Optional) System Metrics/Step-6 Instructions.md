# **Overview**

Built into the PODs is some simple monitoring functionality that can be disabled as it is not required for LoRaWAN to function. This feature leverages Prometheus to collect metric data about the computer, Chirpstack, and ThingsBoard. We utilize Grafana to display the data.

The metrics can be protected behind the local network or exposed to the Internet through a Cloudflare tunnel. In either case, a Grafana dashboard username and password protect accessing the metric data.

These options are set in the POD configuration file.

# **Steps**

