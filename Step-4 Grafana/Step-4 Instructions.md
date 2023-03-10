# **Overview**

Within the pea-PODs architecture Grafana serves the purpose of the Data visualizer. Refer back to this [diagram](https://github.com/adamschreck/pea-pod#diagram-describing-pea-pod-architecture) for more context on what that means. Essentially, Granfana is a tool that turns the device data stored in the PostgresSQL database created by Chirpstack into graphs and visualizations that can be easily interpreted by viewers. Granfana is easily customizable, and examples of dashboards that you can copy from can be found [here](https://grafana.com/grafana/dashboards/) on their community dashboards page. 

# **Steps**

## Getting Started

The steps and figures in this section are almost fully sourced directly from an article on PiMyLifeUp written by the user Emmet titled "Setting up Grafana on the Raspberry Pi" and can be found at [this link](https://pimylifeup.com/raspberry-pi-grafana/). His description explains the purpose of each step while also providing the necessary Terminal commands.

### Installing Grafana to the Raspberry Pi

1. Before we get started with installing Grafana to the Raspberry Pi, we should first ensure all the currently installed packages are up to date.

We can do this by running the following two commands. These commands will update the package list and then upgrade all installed packages to their latest versions.

    sudo apt update
    sudo apt upgrade

2. To install Grafana to the Raspberry Pi, we need to add the Grafana package repository.

Before we can add the repository, we have to add the APT key. The APT key is used to verify the packages actually came from the Grafana package server and have been signed correctly.

To add the Grafana APT key to your Raspberry Pi’s keychain, run the following command.

    curl https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /usr/share/keyrings/grafana-archive-keyrings.gpg >/dev/null

3. With the key added, we can now safely add the Grafana repository to our Pi’s list of packages sources.

Use the following command on your Raspberry Pi to add the repository to the list.

    echo "deb [signed-by=/usr/share/keyrings/grafana-archive-keyrings.gpg] https://apt.grafana.com stable main" | sudo tee /etc/apt/sources.list.d/grafana.list

When you run and update your Raspberry Pi will now automatically read from the Grafana repository for packages.

4. As we have made changes to our package list, we need to run an update.

Running an update with apt allows it to fetch the latest list of packages from all sources.

To do this, use the following command on your Pi’s terminal.

    sudo apt update

5. Our Raspberry Pi should now be aware that Grafana is an available package for the device.

We can install the latest version of Grafana by running the following command on your device.

    sudo apt install grafana

6. Our next step is to get Grafana to start at startup. Luckily for us, Grafana comes with a systemd service file.

To enable Grafana to start at boot, all we need to do is run the following command.

    sudo systemctl enable grafana-server

This command will tell the systems service manager to enable the service file called “grafana-server.service”.

The service manager will use this file as a guide on how to deal with the Grafana server.

7. Finally, let’s start up the Grafana server software.

Run the command below in the Pi’s terminal.

    sudo systemctl start grafana-server

### Connecting to your Raspberry Pi Grafana Installation

1. Similar to Chirpstack, Grafana can be accessed in one of two ways:

- If you are connected to the same internet as the Pi, then visit `your Pi's IP address:3000` in your browser. The 3000 refers to what is known as the "port number", which identifies where that program is running on the device of the IP address given.

  - For example: `10.0.0.145:3000`

 In this case it is saying that the Chirpstack program is running on port `3000` of the Pi called `10.0.0.145`.

- If you use Cloudflare tunnels, detailed in `Step-5 Instructions`, then you can visit your Chripstack tunnel URL from your browser.

  - For example: `pea-pod-adam-gf.oatscenter.org`

2. The first thing you will see when loading up Grafana is a login screen.

On this screen, you will be able to login using the default admin user that was created when you first installed Grafana to your Raspberry Pi.

The username for this user is “admin” and the password is “admin” (1.). While the default password is super insecure, we can change it in the very next step.

With the username and password entered you can login to Grafana by clicking the “Log In” button (2.).

![Raspberry-Pi-Grafana-01-Initial-Login-Screen Large](https://user-images.githubusercontent.com/126691160/223203765-b140e7c1-5812-4559-aedb-d46de61f3f16.jpeg)

3. When you first log in to the Grafana web interface you will be asked to change the user’s password.

While it is possible to skip this step, we highly recommend that you do not. The default password is incredibly insecure and should be changed immediately.

To proceed to the Grafana dashboard, go ahead and enter a new password (1.) then click the “Save” button (2.).

![Raspberry-Pi-Grafana-02-Initial-Setup-Set-New-Password Large](https://user-images.githubusercontent.com/126691160/223204049-b25a84c9-2f96-486c-922f-73522d5e33e2.jpeg)

4. Once you have logged in and changed the default password, you should now be greeted with the following screen.

This screen means that you are now ready to start adding data sources and setting up your Grafana dashboard on your Raspberry Pi.

![Raspberry-Pi-Grafana-03-Initial-Setup-Complete Medium](https://user-images.githubusercontent.com/126691160/223205062-e4f26e85-6c5c-4d75-beb3-60b5e336cfbc.jpeg)

## Setting up Data Source

1. On the bottom left locate the settings icon and navigate to the `Data Sources` section

![Screen Shot 2023-03-06 at 2 23 30 PM](https://user-images.githubusercontent.com/126691160/223210593-fc883c7e-766a-47ae-a70b-617d7e8bb418.png)

2. Currently this page will be empty as there are not any Data Sources setup yet, to add one select `ADD Data Source` 

![Screen Shot 2023-03-06 at 2 23 01 PM](https://user-images.githubusercontent.com/126691160/223211068-21cc23c1-409d-411e-9d1d-921cc02478af.png)

3. Scroll through the available options and choose PostgresSQL

4. After selecting this, PostgresSQL should appear in the data sources list. Select the PostgresSQL source and it will prompt the screen below. Enter in the settings as shown, if you have followed all of the instructions thus far, then the Database will be `chirpstack_as_events` the User will be `chirpstack_as_events` and the Password will be `dbpassword` as configured [here](https://github.com/adamschreck/pea-pod/blob/main/Step-2%20Chirpstack/Step-2%20Instructions.md#activate-the-integration)

![Screen Shot 2023-03-06 at 2 24 05 PM](https://user-images.githubusercontent.com/126691160/223213109-01dd97af-fbf7-476e-9141-0196b929a9b5.png)

5. At the bottom select `Save & test` to save this data source.