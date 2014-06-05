# Green Bean
**An Adapter for the Appliance Maker Community**

The [Green Bean](http://firstbuild.com/greenbean) is a hardware adapter that provides a USB interface to General Electric appliances. This allows devices such as a laptop or a [Raspberry Pi](http://www.raspberrypi.org) to easily connect with, and control, General Electric appliances. For the purpose of this guide, we will be assuming that you will be connecting an appliance to your laptop using the Green Bean.

## Overview

1. [Getting Started](#getting-started)
  - [Connecting the Green Bean to an Appliance](#connecting-the-green-bean-to-an-appliance)
  - [Connecting the Green Bean to a Laptop](#connecting-the-green-bean-to-a-laptop)
  - [Installing the Software](#installing-the-software)
2. [Using the Green Bean Software](#using-the-green-bean-software)
  - [Reading the Cycle Status of the Dishwasher](#reading-the-cycle-status-of-the-dishwasher)
  - [Starting a Cook Mode on the Oven](#starting-a-cook-mode-on-the-oven)
  - [Receiving a Temperature Alert from the Refrigerator](#receiving-a-temperature-alert-from-the-refrigerator)
  - [Receiving an End of Cycle Notification from the Dryer](#receiving-an-end-of-cycle-notification-from-the-dryer)

### Getting Started
There are a few steps that must be performed before we will be able to start controlling an appliance.

#### Connecting the Green Bean to an Appliance
The Green Bean must be connected to the appliance with an RJ45 cable. Any off-the-shelf ethernet cable should work. **It is important not to use a crossover cable as this may damage the Green Bean**. The RJ45 port is in a different location for each appliance, and can be located by referencing [this table](#rj45-locations).

#### Connecting the Green Bean to a Laptop
The Green Bean must be connected to your laptop with a USB micro cable. Again, any off-the-shelf USB micro cable should work. The Green Bean is powered over USB and should appear as a USB HID device on your laptop shortly after it is plugged in.

#### Installing the Software
The software that controls the Green Bean and communicates with the appliances must be installed before you can start developing applications to control your appliance. If you have not already, please download and install [node.js](http://nodejs.org/download) and then install the Green Bean software by running the following command from a terminal.

```
npm install green-bean
```

### Using the Green Bean Software
To demonstrate the features of the Green Bean, I will show how easy it is to connect to an appliance and start communicating with it. Below are a few node.js applications that demonstrate how to communicate with, and control, an appliance.

#### Reading the Cycle Status of the Dishwasher
Below is an example of how to read the cycle status of the dishwasher. For a more in-depth look at this example, see the [cycle status](https://github.com/GEMakers/gea-plugin-dishwasher#dishwashercyclestatus) documentation.

``` javascript
var greenBean = require("green-bean");

greenBean.connect("dishwasher", function (dishwasher) {
    dishwasher.cycleStatus.read(function (value) {
        console.log("cycle status:", value);
    });
});
```

#### Starting a Cook Mode on the Oven
Below is an example of how to start a cook mode on an oven. For a more in-depth look at this example, see the [cook mode](https://github.com/GEMakers/gea-plugin-range#rangeupperovencookmode) documentation.

``` javascript
var greenBean = require("green-bean");

greenBean.connect("range", function (range) {
    range.upperOven.cookMode.write({
        mode: 18,
        cookTemperature: 350,
        cookHours: 1,
        cookMinutes: 0
    });
});
```

#### Receiving a Temperature Alert from the Refrigerator
Below is an example of how to subscribe to temperature alerts for a refrigerator. For a more in-depth look at this example, see the [temperature alert](https://github.com/GEMakers/gea-plugin-refrigerator#temperature-alert) documentation.

``` javascript
var greenBean = require("green-bean");

greenBean.connect("refrigerator", function (refrigerator) {
    refrigerator.temperatureAlert.subscribe(function (value) {
        console.log("temperature alert:", value);
    });
});
```

#### Receiving an End of Cycle Notification from the Dryer
Below is an example of how to subscribe to an end of cycle notification from a dryer. For a more in-depth look at this example, see the [end of cycle](https://github.com/GEMakers/gea-plugin-laundry#laundryendofcycle) documentation.

``` javascript
var greenBean = require("green-bean");

greenBean.connect("laundry", function (laundry) {
    laundry.endOfCycle.subscribe(function (value) {
        console.log("end of cycle:", value);
    });
});
```
