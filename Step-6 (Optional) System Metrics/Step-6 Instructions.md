# **Overview**

After you have completed the setup of your Pi and subsequent LoRaWAN network, it be me important to look at how your Pi is performing. Specifically, because all of your data will live locally on the Pi it is advisable that you monitor the storage and available space left for data storage. To do this two tools called Prometheus and Node Exporter can run constantly on the Pi to collect system metrics, then a new Grafana dashboard can visualize these measurements.

# **Steps**

## Getting Started

The steps and figures in this section are almost fully sourced directly from an article on PiMyLifeUp written by the user Emmet titled "Installing Prometheus on the Raspberry Pi" and can be found at [this link](https://pimylifeup.com/raspberry-pi-prometheus/). His description explains the purpose of each step while also providing the necessary Terminal commands.

### Downloading Prometheus

1. Before we proceed, we should ensure that all of our packages are up to date.

Doing this ensures we are installing everything from a clean base, and any out of date packages shouldn’t be causing issues.

To upgrade all currently installed packages, run the following command on your Raspberry Pi

    sudo apt update
    sudo apt full-upgrade

2. We can download the pre-compiled version of Prometheus for the ARMv7 architecture.

To download this software, run the following command on your software.

    wget https://github.com/prometheus/prometheus/releases/download/v2.22.0/prometheus-2.22.0.linux-armv7.tar.gz

This command will use wget to download the 2.22.0 version of Prometheus to your Raspberry Pi.

3. Extract the binaries outside of the archive you downloaded by running the following command.

We can use the tar program to extract our archive.

    tar xfz prometheus-2.22.0.linux-armv7.tar.gz

4. Our next step is to rename the extracted folder to remove the version from the folder name.

Doing this makes it easier to reference the files within the directory. Use the mv command to rename the directory to prometheus.

    mv prometheus-2.22.0.linux-armv7/ prometheus/

5. Our final step is to clean up our installation.

All we need to do is delete the archive we downloaded earlier. While it is safe to keep, there is no longer any need to have the file around.

Delete the Prometheus archive by running the following command on your Raspberry Pi.

    rm prometheus-2.22.0.linux-armv7.tar.gz

With that done, we now have Prometheus installed on our Raspberry Pi.

### Setting Up a Service for Prometheus

1. To create a service, we need to create a new file within the “/etc/systemd/system/” directory.

This directory is where services are handled by default.

To create this file, we will be using the nano text editor.

Begin writing the new service file by running the following command on your Pi.

    sudo nano /etc/systemd/system/prometheus.service

2. Within this file, enter the following text.

The text defines how the service works and how it should run the Prometheus software.

    [Unit]
    Description=Prometheus Server
    Documentation=https://prometheus.io/docs/introduction/overview/
    After=network-online.target

    [Service]
    User=pi
    Restart=on-failure

    ExecStart=/home/pi/prometheus/prometheus \
    --config.file=/home/pi/prometheus/prometheus.yml \
    --storage.tsdb.path=/home/pi/prometheus/data

    [Install]
    WantedBy=multi-user.target

With the way this service file is written, it will run the Prometheus software on your Raspberry Pi once the network has come online.

Upon starting up, it will run the Prometheus executable located at “/home/pi/prometheus/prometheus“.

We pass in both the config file location and a storage location for the database that the monitoring software requires.

If you ever need to modify the config file, you can find it at “/home/pi/prometheus/prometheus.yml“.

2. Once you have finished writing to the service file, save it.

You can save and quit out of the file by pressing `control` + `X` or `^X` then `Y` for yes and `enter`.

3. With the new service created, we can now go ahead and enable it.

To enable the Prometheus service, we can run the following command.

    sudo systemctl enable prometheus

Enabling the service is what allows it to start when the Raspberry Pi boots up.

4. With the service enabled, let us now start the Prometheus software up.

To start the service, run the following command

    sudo systemctl start prometheus

5. We can verify that Prometheus has successfully started on our Raspberry Pi by checking its status.

Type the following command on your Raspberry Pi to retrieve the status of the service.

    sudo systemctl status prometheus

6. If everything has started up correctly, you should see the following returned by the status command.

    `Active: active (running)`

### Installing Node Exporter

1. The first thing we need to do is create a new directory in the “/opt” by using the command below.

This directory is where we will keep the node exporter as the location is intended for packages not provided by the OS’s distribution.

    sudo mkdir /opt/node-exporter

2. Next, change into our newly-created directory.

Changing to the directory will ensure that the archives we are about to download will be in the correct place.

    cd /opt/node-exporter

3. Our next step is to download the archive for the Prometheus node exporter to our device.

The version that you want to download changes based on your device. For example, as we are using a Raspberry Pi 4, we will want to download the ARMv7 of the Prometheus exporter.

    sudo wget -O node-exporter.tar.gz https://github.com/prometheus/node_exporter/releases/download/v1.0.1/node_exporter-1.0.1.linux-armv7.tar.gz

4. With the archive of Prometheus downloaded to your device. We can now use the tar package to extract it.

Run the following command to extract the archive into the current directory.

    sudo tar -xvf node-exporter.tar.gz --strip-components=1

We use the “strip-components” option to only get the files within the archive and not the top-level directory.

5. With the Prometheus node exporter extracted to our device, we can now delete the archive.

Run the following command to delete the archive.

    sudo rm node-exporter.tar.gz

Deleting the archive isn’t necessarily needed, but it helps keep your system clean of unneeded files.

6. Finally, we can bring the node exporter online by using the command below.

    ./node_exporter

### Setting Up Node Exporter as a Service

1. Let us start by writing the file that will define our service.

Run the following command to begin writing to a new file.

    sudo nano /etc/systemd/system/nodeexporter.service

2. Within this file, type in the following lines of code.

    [Unit]
    Description=Prometheus Node Exporter
    Documentation=https://prometheus.io/docs/guides/node-exporter/
    After=network-online.target

    [Service]
    User=pi
    Restart=on-failure

    ExecStart=/opt/node-exporter/node_exporter

    [Install]
    WantedBy=multi-user.target

3. Once you have finished writing to the service file, save it.

You can save and quit out of the file by pressing `control` + `X` or `^X` then `Y` for yes and `enter`.

4. With the service now saved, we should now enable it.

Running the following command will let our node exporter startup when the device powers on.

    sudo systemctl enable nodeexporter

5. Next, let’s start the Prometheus node exporter now, so we don’t have to wait until we restart.

    sudo systemctl start nodeexporter

### Adding to Prometheus Node

1. Let us start this process by editing the Prometheus configuration file.

You can begin editing this file by using the command below on your Raspberry Pi.

    nano /home/pi/prometheus/prometheus.yml

2. Within this file, you will see a series of lines that define how Prometheus will work.

The bit that we are interested in is the “scrape_configs” section. This section is what will allow us to add additional jobs to scrape from.

For example you can add this:

    static_configs:
        - targets: ['localhost:9090']
        - job_name: 'node1'

    static_configs:
        - targets: ['localhost:9100']

And your file should appear like this example: 

![Screen Shot 2023-03-06 at 3 33 37 PM](https://user-images.githubusercontent.com/126691160/223227079-436d415a-5e35-46b3-aa59-0ca396e42f32.png)

3. Once you have finished writing to the service file, save it.

You can save and quit out of the file by pressing `control` + `X` or `^X` then `Y` for yes and `enter`.

4. As we have made changes to the Prometheus configuration, we need to restart the software.

As we have already created a service for it on our Raspberry Pi, restarting is as simple as running the following command.

    sudo systemctl restart prometheus

### Setting up Grafana Dashboard

1. From the left panel within Grafana hover over the `dashboards` icon and select `+immport` from the list

![Screen Shot 2023-03-06 at 10 55 14 PM](https://user-images.githubusercontent.com/126691160/223317247-089f3a9c-78d8-47b5-b52a-786dd73b8994.png)

2. Once `+immport` is selcted it will lead to the page shown below. From here we can import a pre-made dashboard designed for Prometheus and Node Exporter metrics from the Grafana dashboards community. More information about the specific dashboard that we will use can be found [here](https://grafana.com/grafana/dashboards/1860-node-exporter-full/). To import, within the box below `Import via grafana.com` enter the ID `1860` and click `Load`.

![Screen Shot 2023-03-06 at 10 56 40 PM](https://user-images.githubusercontent.com/126691160/223317182-3f9dfdcf-e8ea-4862-9430-a105e97c9feb.png)

The final product should appear as shown in the image below. A number of metrics are shown and not all hold the same value for the pea-POD applicaiton, but expand the `Basic CPU / Mem / Net / Disk` accordian to view memory specific data.

![Screen Shot 2023-03-06 at 11 02 40 PM](https://user-images.githubusercontent.com/126691160/223317751-4f3213ec-9d68-4666-b681-a4fb1c5d5c87.png)


