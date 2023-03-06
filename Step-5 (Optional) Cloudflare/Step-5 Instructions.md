# **Overview**

All POD's network services are only accessible by computers connected to the same network. That could be a computer or mobile device connected to the POD's local Wi-Fi network or a device connected to the same Wi-Fi network that the POD connects. In other words, the data stored on a POD can not be accessed from the Internet, even if the POD has Internet access.

Cloudflare tunnels fix that. Through the use of a Cloudflare tunnel, the POD services can be accessed from anywhere in the world via the Internet in a selected and controlled way. For example, you could expose ThingsBoard which would allow you to view your data, after entering your username and password, from anywhere. Chripstack, monitoring services, and SSH can also be exposed to afford easier device management, software upgrading, and real-time POD monitoring.

This optional feature can be enabled in the POD configuration file and does require a free Cloudflare account that manages a private domain. Please consult the configuration file and the Cloudflare website for more details

# **Steps**
