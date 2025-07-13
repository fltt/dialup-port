Dial-Up Utilities
=================
The *Dial-Up Utilities* is a collection of scripts and configuration
files meant to manage GSM/UMTS/LTE (a.k.a. 2G/3G/4G) network adapters.
These devices are usually removable USB dongles/sticks with a (U)SIM
(Universal Subscriber Identity Module) slot.

Features
--------
The *Dial-Up Utilities* provide the following features:

* register/configure the network adapter when plugged
* unlock the SIM
* start and stop the connection to the mobile network
* update resolver DNS servers
* keep account of the available network traffic
* store/retrieve accounting of network traffic in/from the SIM's memory
* manage multiple network adapters
* automatically stop the connection when the montly traffic quota is
  over

Build and install
-----------------
To build and install the package:

```
cd path/to/dialup-port/dialup
make install
```

You will be asked to enter `root`'s password to gain write access to the
`PORT_DBDIR` directory and to install the built package.

If you want to build the package as a regular user, just redefine the
`PORT_DBDIR` variable, e.g.:

```
cd path/to/dialup-port/dialup
export PORT_DBDIR="$HOME/ports/db"
make package
```

> **NOTE:** To install the package you still need `root` privileges.

For more information about the available `make` targets and the *FreeBSD
Port Collection*, see `ports(7)`.
