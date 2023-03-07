# **Overview**

All POD's network services are only accessible by computers connected to the same network. That could be a computer or mobile device connected to the POD's local Wi-Fi network or a device connected to the same Wi-Fi network that the POD connects. In other words, the data stored on a POD can not be accessed from the Internet, even if the POD has Internet access.

Cloudflare tunnels fix that. Through the use of a Cloudflare tunnel, the POD services can be accessed from anywhere in the world via the Internet in a selected and controlled way. For example, you could expose Grafana which would allow you to view your data, after entering your username and password, from anywhere. Chripstack, monitoring services, and SSH can also be exposed to afford easier device management, software upgrading, and real-time POD monitoring.

This optional feature can be enabled in the pea-POD, but does require a free Cloudflare account that manages a private domain. The steps below will detail one way to setup your own free domain (if you do not already own one), register for a Cloudflare account, download Cloudflare to the Pi, and how to tie all of these elements together.

# **Steps**

## Signing up for Cloudflare

[Visit this link](https://dash.cloudflare.com/sign-up) to sign up for your own Cloudflare account. Be sure to keep an eye on your email for a message to verify your account. 

![Screen Shot 2023-03-07 at 11 26 54 AM Medium](https://user-images.githubusercontent.com/126691160/223487213-b526434c-1fa8-4f02-a818-ab0d1b93740f.jpeg)


## Registering a Domain

There are several options for registering your own domain name. Both paid and free domains can be found depending on what you want your domain name to be called. In truth, your Cloudflare account simply needs a domain and it does not necessarily matter what it is called. With these needs in mind, this section will detail two methods to register your own domain. The first may not necessarily be an option, so ensure that you read both descriptions before moving forward with any actions.

### Option 1: Freenom and the extension .tk

Freenom is a site that allows for the registrarion of domains using the few extensions that offer free domain registrations, one of these being `.tk` which you can register for up to one year at a time. At the time of creating the domain for the first pea-POD the steps below were used. However after recently visiting Freenom it appears that they are having technical issues with new registrations. At the time of your access these issues may be resolved, if not it is suggested that you use the next option's steps.

1. Sign into [Freenom](https://my.freenom.com/clientarea.php) using your Google or Facebook account. There are other ways to create an account, however this involves the least amount of complication.

![Screen Shot 2023-03-07 at 9 20 45 AM Medium](https://user-images.githubusercontent.com/126691160/223450825-10388985-50ed-41f2-be8d-e6cdb24d5074.jpeg)

2. Once you have signed in, hover over `Services` and within its drop-down select `Register a New Domain`.

![Screen Shot 2023-03-07 at 9 27 22 AM Medium](https://user-images.githubusercontent.com/126691160/223451528-0fe5a5ba-7db7-4e22-963e-248c3a57ac40.jpeg)

3. From the `Find your new Domain` box search your desired domain with the extsion .tk added to the end and click `Check Availability`. See the image below as an example. Your desired domain may or may not be available for registration. If you do not search with the extension `.tk` at the end Freenom will always say that that name is taken, even if the domain is truly available.

![Screen Shot 2023-03-07 at 9 32 46 AM](https://user-images.githubusercontent.com/126691160/223465748-c07c7a31-b225-4951-b1c0-7574258bac55.png)

4. With an available domain name selected, follow the on screen prompts of Freenom to add the domain to your cart and checkout for free.

5. To confirm that this process has been completed, you can hover over `Services` and within its drop-down select `My Domains`. The final result should appear as shown below.

![Screen Shot 2023-03-07 at 10 33 59 AM](https://user-images.githubusercontent.com/126691160/223470164-4852e522-8b60-49b4-8a0c-0ac9c770de5c.png)


### Option 2: Paid Domains

In truth there are not many free ways to register a domain name today. If Freenom and extensions such as .tk are not available, then there are essentially no truly free domain options. As an alternative, you can use any number of domain registration sites such as Google Domains. By paying you will have more choice on the name and can hold the registration for longer than the terms of Freenom. Prefered sites for paid domain registration can be found below. 

#### gen.xyz and the extension .xyz

The benefit of gen.xyz is that they offer what are called 1.111B Class domains, which are numerical domain names that cost just $0.99 per year. Despite appearing somewhat random or not as simple as non-numerical names, the Cloudflare will operate the same no matter the domain name. This is the lowest cost option if free sources are not available. [At this link](https://gen.xyz/1111b) you can search for names and follow the steps to secure your domain. In the image below you can see more pricing information. 

![Screen Shot 2023-03-07 at 10 48 55 AM Medium](https://user-images.githubusercontent.com/126691160/223476576-9e793a3e-7107-409b-88be-eee8c380c1ed.jpeg)

#### Cloudflare Domains

In addition to other services, Cloudflare offers the ability to purchase domains through your account. While slightly more expensive than the gen.xyz option, Cloudflare allows more choices in what your domain name will be and what extension it will use. This allows for non-numerical domains and domains that may be more in line with your project such as `pea-pods-adam.com`. Depending on your preferences you could find multiple domains for well less than $10 per year. 

While signed into your Cloudflare account, and with your email verified, you can look to the left tool bar for `Domains Registration`. Expand this accordian to reveal the various options, and select `Register Domains`. From this page in the box under `Enter a domain name` type a domain name that you are interested in purchasing, then click `Search`. Now a table with your options should appear. Choose the best domain for you and click `Purchase`, then follow through with your transaction. 

![Screen Shot 2023-03-07 at 11 14 51 AM Medium](https://user-images.githubusercontent.com/126691160/223486823-bd0099e4-dbd5-42ab-90cb-46ba512aa59a.jpeg)

### Assigning a Domain as a Website

If you did not purchase your domain through Cloudflare, you must add it in as a website. Do this by navigating to the `Webistes` page on left tool bar.

![Screen Shot 2023-03-07 at 2 20 23 PM](https://user-images.githubusercontent.com/126691160/223529866-b6b9b573-73e6-4ffb-99bd-cc72a21f0293.png)

On this page click `+Add a Site`

![Screen Shot 2023-03-07 at 2 20 49 PM](https://user-images.githubusercontent.com/126691160/223531603-fb60db0e-b167-40ae-9684-aa772030d0c8.png)

In the box under `Enter your site (example.com)` type in your registered domain, then click `Add Site` button to add it as one of your websites. Now when clicking the `Webistes` page on left tool bar, when the `Home` page is prompted it should display a box with your domain. By clicking that box you can look at settings, data, management tools that are pertinent to your website.

![Screen Shot 2023-03-07 at 2 33 22 PM](https://user-images.githubusercontent.com/126691160/223533060-3562f604-1577-4329-8172-754adc89e7fe.png)

## Connecting your Pi and Cloudflare

The steps and figures in this section are almost fully sourced directly from an article on PiMyLifeUp written by the user Emmet titled "Setting up a Cloudflare Tunnel on the Raspberry Pi" and can be found at [this link](https://pimylifeup.com/raspberry-pi-cloudflare-tunnel/). His description explains the purpose of each step while also providing the necessary Terminal commands.


### Adding Cloudflare to Pi

1. Our first task is to perform an update of the package list as well as upgrade any out-of-date packages.

You can perform both of these tasks using the following command in the terminal.

    sudo apt update
    sudo apt upgrade

2. Once the update completes, we must ensure we have both the `curl` and `lsb-release` packages.

Install both of these packages by using the command below in the terminal.

    sudo apt install curl lsb-release

`curl` – We will use curl to grab the GPG key for the Cloudflared repository.
`lsb-release` – This package allows us to easily retrieve information about the system, such as the release name.

3. With all the required packages in place, we can finally grab the GPG key for the Cloudflared repository and store it on our Raspberry Pi.

To save this key to your device, use the following command.

    curl -L https://pkg.cloudflare.com/cloudflare-main.gpg | sudo tee /usr/share/keyrings/cloudflare-archive-keyring.gpg >/dev/null

A GPG key is crucial to verify the packages we are installing are valid and belong to the repository.

4. With the GPG key saved into our keyrings folder, our next step is to add the Cloudflared repository to our Raspberry Pi. 

You can add:

    echo "deb [signed-by=/usr/share/keyrings/cloudflare-archive-keyring.gpg] https://pkg.cloudflare.com/cloudflared $(lsb_release -cs) main" | sudo tee  /etc/apt/sources.list.d/cloudflared.list

5. As we have made changes to the available repositories, we will need to perform another update of the package list cache,

You can update this cache by using the following command within the terminal.

    sudo apt update

6. With the repository added, we can now proceed to install the Cloudflared package to our Raspberry Pi.

To install this package, you will want to run the following command.

    sudo apt install cloudflared

### Setting up a Tunnel

1. Our first step is to create an association between our Raspberry Pi and the Cloudflare service.

We can begin authenticating with the Cloudflare service by using the command below.

    cloudflared tunnel login

Ensure you keep Cloudflared open on your device while this process is completed.

2. After running the above command, you will see the following message appear within the terminal.

You will want to go to the URL displayed in the message and use it to log in to your Cloudflare account.

`Please open the following URL and log in with your Cloudflare account:https://dash.cloudflare.com/argotunnel?callback=https%3A%2F%2Flogin.cloudflareaccess.org%2FXXXXXXXXXX Leave cloudflared running to download the cert automatically.`

3. Once your Raspberry Pi is successfully authenticated with the Cloudflare service, you will see the following message.

`You have successfully logged in. If you wish to copy your credentials to a server, they have been saved to: /home/pi/.cloudflared/cert.pem`

4. Now that we are authorized, we can create a Cloudflare tunnel by using the following command.

Ensure you replace `TUNNELNAME` with the name you want to assign this tunnel. For example you could use `pea-pod-gateway`. 

    cloudflared tunnel create TUNNELNAME

**OR**

    cloudflared tunnel create pea-pod-gateway

5. After running the above command, you will see a message similar to the one below.

You will want to write down the ID as we will need this for later.

`Tunnel credentials written to /home/pi/.cloudflared/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.json. cloudflared chose this file based on where your origin certificate was found. Keep this file secret. To revoke these credentials, delete the tunnel.`

6. With the tunnel created, we can now route the tunnel to a domain name that we have with Cloudflare. This will allow us to access our Raspberry Pi through that domain name.

Ensure you replace `TUNNELNAME` with the name of your tunnel and replace `DOMAINNAME` with the domain name you want to use.

    cloudflared tunnel route dns TUNNELNAME DOMAINNAME

7. If the above command worked correctly, you would see a similar message to the one below. This message confirms that Cloudflare created a CNAME that routes to your tunnel.

`2022-10-18T04:54:54Z INF Added CNAME DOMAINNAME which will route to this tunnel tunnelID=XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX`

8. The final task we need to do is connect the Cloudflare tunnel to a destination on our Raspberry Pi.

While the tunnel exists, it isn’t currently linked to anything, so in this example we will be putting it to a specific URL.

You will likely want it to be started when your Raspberry Pi starts. To do this, we will have to write all of this within a `config.yml` file that the Cloudflare daemon will read.

    sudo nano ~/.cloudflared/config.yml

9. Within this file, you will want to type in the following lines and adjust them for your use case as you go.

Keep these terms in mind: 

[TUNNELNAME] – Replace this value with the name of your tunnel.
[USERNAME] – This value will need to be replaced with your user’s name.
[UUID] – You will need to specify the UUID that you got back in step 5 of this section.
[HOSTNAME] – Swap this value out with the domain name you are planning to utilize. For example, “test.pimylifeup.com“.
[PORT] – Finally, replace “PORT” with the port you want accessible through the tunnel.
[PROTOCOL] – This is the protocol you want tobe utilized for your service. In the case of a web server, you will want to use “http” or “https“.

Your file should appear as this:

    tunnel: [UUID]
    credentials-file: /home/[USERNAME]/.cloudflared/[UUID].json

    ingress:
        - hostname: [HOSTNAME]
        service: [PROTOCOL]://localhost:[PORT]
        - service: http_status:404



An example with the correct default ports for Chirpstack, Grafana, and SSH would look like this: 

    tunnel: [UUID from step 5]
    credentials-file: /root/.cloudflared/[UUIDfromstep5].json

    ingress:
    - hostname: pea-pod-chirpstack.[YOUR DOMAIN NAME]
        service: http://localhost:8080
    - hostname: pea-pod-ssh.[YOUR DOMAIN NAME]
        service: ssh://localhost:22
    - hostname: pea-pod-grafana.[YOUR DOMAIN NAME]
        service: http://localhost:3000
    - service: http_status:404

10. To exit nano and save the changes you can follow the commands listed at the bottom. In the case of Mac the sequence is `control` + `X` or `^X` then `Y` for yes and `enter`

11. With the config file created, we can install it as a service using the following command.

This command will copy our config file to the correct location and prepare a service file for systemd.

    sudo cloudflared --config ~/.cloudflared/config.yml service install

12. We can enable the Cloudflare tunnel service so that it will start when our Raspberry Pi does.

To do this use the following command.

    sudo systemctl enable cloudflared

13. You can ensure the tunnel is online now by using the command below.

 Within the terminal: 

    sudo systemctl start cloudflared

14. Finally, you can visit any of the links within your config file in a browser. From the example config file, if I were to type `pea-pod-grafana.[YOUR DOMAIN NAME]` into a browser it should pull up the Grafana for that Pi. If this works as intended then you can now access your data from anywhere as long as your Pi is connected to Internet!

To look at and manage your tunnel from the Cloudflare website click the `Zero Trust` section from the left tool bar. 

![Screen Shot 2023-03-07 at 2 35 35 PM](https://user-images.githubusercontent.com/126691160/223533507-d179c2d3-a5ae-44f7-af06-d37193c3c6d4.png)

This will prompt an entirely new tab. From the left tool bar in the new `Cloudflare Zero Trust` tab find the `Access` section, expand its accordian, and select `Tunnels`.

From here you should see the tunnel that you created on your Pi, and navigating to this page can tell you key information like the status of your tunnel. Changes, such as changing your routes, made to your tunnel here ***should** translate down to the config file on your Pi. THIS IS NOT ALWAYS THE CASE. It is suggested that you only make modifications from the actual config file. 





