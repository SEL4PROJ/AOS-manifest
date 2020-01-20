<!-- @TAG(DATA61_BSD) -->

AOS Project Repository Manifest
===============================

This is the staging project for the Advanced Operating Systems project.

This repository is made available publicly and can be used directly to
set up the project using the `repo` tool.

The Advanced Operating Systems project
--------------------------------------

This project supports the practical component of the [COMP9242:
Advanced Operating Systems](https://www.cse.unsw.edu.au/~cs9242/)
course.

The [project specification](https://www.cse.unsw.edu.au/~cs9242/current/project/index.shtml)
describes the milestones students work through using this code in the
course.

General use of seL4 project manifest repositories
-------------------------------------------------

For general instructions on using this repository, see [Getting Started](https://docs.sel4.systems/GettingStarted)
and the [seL4Test page](https://docs.sel4.systems/seL4Test).

See [Host Dependencies](https://docs.sel4.systems/HostDependencies) for
required dependencies.

System setup for the Advanced Operating Systems project
-------------------------------------------------------

A guide for configuring a Linux host is described in the [linux setup
guide](https://www.cse.unsw.edu.au/~cs9242/current/project/linux.shtml)
on the course website.

The project makes a number of assumptions regarding the setup used:

* The hardware platform used is an
  [ODroid-C2](https://www.hardkernel.com/shop/odroid-c2/).
* The ODroid-C2 is configured to boot with the following configuration:

  ```
  # Autoboot configuration
  bootdelay=1
  bootcmd=tftp ${sel4_addr} ${sel4_image} && go ${sel4_addr}
  sel4_addr=0x10000000
  sel4_image=sos-image-arm-odroidc2

  # IP configuration
  gatewayip=192.168.168.1
  netmask=255.255.255.0
  ipaddr=192.168.168.2

  # TFTP Server
  serverip=192.168.168.1
  ```
* The serial device `/dev/ttyUSB0` on the host is a USB serial device
  connected to the ODroid-C2's primary UART interface.
* The host is configured on a common network with the ODroid-C2 with
  the IP address `192.168.168.1/24` (this is usually done with a
  USB-ethernet adaptor connected directly to the ODroid-C2).
* The host has a TFTP server listening on the `192.168.168.1` interface
  configured with the root directory in `/var/tftpboot/$USER` (where
  `$USER` is the username executing the `reset.sh` script in the root of
  the project).
* The host has a NFS server listening on the `192.168.168.1` interface
  with the `/var/tftpboot/$USER` directory read/write accessible to
  `192.168.168.2`.

Many of the above settings can be re-configured in the two following
files within the repository directory:

* `projects/aos/sos/CMakeLists.txt`
* `projects/aos/reset.sh`
