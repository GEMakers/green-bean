# Green Bean API for the GEA SDK

This node.js package provides functionality for communicating with an appliance via the [Green Bean](http://firstbuild.com/greenbean).

## Table of Contents

- [Installation](#installation)
- [API](#green-bean-api)
  - [bus.on("range", callback)](#busonrange-callback)
    - [range.twelveHourShutoff](#rangetwelvehourshutoff)
- [Appendix](#appendix)
  - [Appliance Type](#appliance-type)

## Installation
To install this application using the node.js package manager, issue the following commands:

```
npm install git+https://github.com/GEMakers/green-bean.git
```

## Green Bean API
Below is the documentation for each of the functions provided by this package, as well as a few examples showing how to use them.

### *greenBean.connect(applianceType, callback)*
Connect to an appliance. Once connected, the appliance object is passed to the callback function.

``` javascript
var greenBean = require("green-bean");

greenBean.connect("range", function (range) {
    console.log("version:", range.version.join("."));
});
```

## Appendix

### Appliance Type
The following is a list of the available appliance Types.

| Appliance Type                                                              |
|:----------------------------------------------------------------------------|
| [range](git+https://github.com/GEMakers/gea-plugin-range.git)               |
| [dishwasher](git+https://github.com/GEMakers/gea-plugin-dishwasher.git)     |
| [refrigerator](git+https://github.com/GEMakers/gea-plugin-refrigerator.git) |
| [laundry](git+https://github.com/GEMakers/gea-plugin-laundry.git)           |
