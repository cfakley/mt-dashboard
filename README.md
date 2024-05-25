# Exporting data from Mastertronic into Grafana 
As a saltwater aquarist I, like many others, have invested money into my hobby. One area of investment for me has been the Mastertronic automated water parameter testing appliance by Focustronic.
The use of this product has been a challenge, and a major component of that challenge has been the use of the mobile app which is used to control, configure, and display testing results.

This project will detail how to extract test results and other data from the Mastertronic and display them on a Grafana dashboard.

There are three components to this:
```
1. Extracting the data from the Mastertronic device.
2. Automating that extraction so that data pulled is kept up to date.
3. Importing the data into Grafana so that it can be used to create a dashboard.
```

# The Mastertronic 
At the heart of the Mastertronic is a Raspberry Pi Zero. This is a small Single Board Computer (SBC) which is used to control all the motors and pumps of the Mastertronic.

This Raspberry Pi Zero is running Raspbian Linux, which is a derivative of Debian Linux and built for Raspberry Pi boards. Fortunately this makes learning about how it works relatively straight forward.

All data for the Mastertronic, including test results, schedules, and reagent vials, are stored in a SQLite Database.

# Prerequisites
There are some prerequisites we will need in order to get this setup. They are:

  - The Mastertronic device (actually the IP address of it). You should be able to find this by connecting to your router.
  - A device to trigger and collect the data export.
  - A device to run Grafana.

Fortunately these last two can be combined into a single device. I am using a computer running Linux, but a Raspberry Pi (or clone) works just as well.

# Data Collection
The Mastertonic has some hidden API's. One of these will dump the contents of the SQLite database and we will use this to export the data.

```
http://{IP of Mastertronic}/api/dump_file
```

# Scheduled Collection

