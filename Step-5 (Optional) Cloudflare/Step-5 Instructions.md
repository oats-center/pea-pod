# **Overview**

All POD's network services are only accessible by computers connected to the same network. That could be a computer or mobile device connected to the POD's local Wi-Fi network or a device connected to the same Wi-Fi network that the POD connects. In other words, the data stored on a POD can not be accessed from the Internet, even if the POD has Internet access.

Cloudflare tunnels fix that. Through the use of a Cloudflare tunnel, the POD services can be accessed from anywhere in the world via the Internet in a selected and controlled way. For example, you could expose Grafana which would allow you to view your data, after entering your username and password, from anywhere. Chripstack, monitoring services, and SSH can also be exposed to afford easier device management, software upgrading, and real-time POD monitoring.

This optional feature can be enabled in the pea-POD, but does require a free Cloudflare account that manages a private domain. The steps below will detail one way to setup your own free domain (if you do not already own one), register for a Cloudflare account, download Cloudflare to the Pi, and how to tie all of these elements together.

# **Steps**

## Registering a Domain

There are several options for registering your own domain name. Both paid and free domains can be found depending on what you want your domain name to be called. In truth, your Cloudflare account simply needs a domain and it does not necessarily matter what it is called. With these needs in mind, this section will detail two method to register your own domain.

### Option 1: Freenom and the extension .tk

Freenom is a site that allows for the registrarion of domains using the few extensions that offer free domain registrations, one of these being `.tk` which you can register for up to one year at a time. At the time of creating the domain for the first pea-POD the steps below were used. However after recently visiting Freenom it appears that they are having technical issues with new registrations. At the time of your access these issues may be resolved, if not it is suggested that you use the next option's steps.

1. Sign into [Freenom](https://my.freenom.com/clientarea.php) using your Google or Facebook account. There are other ways to create an account, however this involves the least amount of complication.

![Screen Shot 2023-03-07 at 9 20 45 AM Medium](https://user-images.githubusercontent.com/126691160/223450825-10388985-50ed-41f2-be8d-e6cdb24d5074.jpeg)

2. Once you have signed in, hover over `Services` and within its drop-down select `Register a New Domain`.

![Screen Shot 2023-03-07 at 9 27 22 AM Medium](https://user-images.githubusercontent.com/126691160/223451528-0fe5a5ba-7db7-4e22-963e-248c3a57ac40.jpeg)

3. From the `Find your new Domain` box search your desired domain with the extsion .tk added to the end. See the image below as an example. Your desired domain may or may not be available for registration. If you do not search with the extension `.tk` at the end Freenom will always say that that name is taken, even if the domain is truly available.

![Screen Shot 2023-03-07 at 9 32 46 AM](https://user-images.githubusercontent.com/126691160/223465748-c07c7a31-b225-4951-b1c0-7574258bac55.png)

4. With an available domain name selected, follow the on screen prompts of Freenom to add the domain to your cart and checkout for free.

5. To confirm that this process has been completed, you can hover over `Services` and within its drop-down select `My Domains`. The final result should appear as shown below.

![Screen Shot 2023-03-07 at 10 33 59 AM](https://user-images.githubusercontent.com/126691160/223470164-4852e522-8b60-49b4-8a0c-0ac9c770de5c.png)


### Option 2: Paid Domains

#### gen.xyz and the extension .xyz

