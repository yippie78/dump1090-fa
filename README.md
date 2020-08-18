# Forked from flightaware/dump1090, 
has missing --net-http-port option, this option comes handy to monitor stats locally.
This repo is work-in-progress, backported code from "MalcolmRobb/dump1090.git". 
--net-http-port (default: 8080) option works however webpage won't show aircrafts even though "handleHTTPRequest" api does send aircraft data.
To verify try http://192.168.xxx.yyy:8080/data.json should show aircraft data, this data.json is called by the api to fwd data via --net-http-port

# use manual build command to turn on/off this feature
"make BLADERF=no HTTP=no"                 - will disable bladeRF and --net-http-port support and remove their dependency

"make BLADERF=no"                         - will disable bladeRF but enable --net-http-port support.


# ********** No change from flightaware/dump1090 *****************
# dump1090-fa Debian/Raspbian packages

This is a fork of [dump1090-mutability](https://github.com/mutability/dump1090)
customized for use within [FlightAware](http://flightaware.com)'s
[PiAware](http://flightaware.com/adsb/piaware) software.

It is designed to build as a Debian package.

## Building under stretch

```bash
$ sudo apt-get install build-essential debhelper librtlsdr-dev pkg-config dh-systemd libncurses5-dev libbladerf-dev
$ dpkg-buildpackage -b
```

## Building under jessie

### Dependencies - bladeRF

You will need a build of libbladeRF. You can build packages from source:

```bash
$ git clone https://github.com/Nuand/bladeRF.git  
$ cd bladeRF  
$ git checkout 2017.12-rc1  
$ dpkg-buildpackage -b
```

Or Nuand has some build/install instructions including an Ubuntu PPA
at https://github.com/Nuand/bladeRF/wiki/Getting-Started:-Linux

Or FlightAware provides armhf packages as part of the piaware repository;
see https://flightaware.com/adsb/piaware/install

### Dependencies - rtlsdr

This is packaged with jessie. `sudo apt-get install librtlsdr-dev`

### Actually building it

Nothing special, just build it (`dpkg-buildpackage -b`)

## Building under wheezy

First run `prepare-wheezy-tree.sh`. This will create a package tree in
package-wheezy/. Build in there (`dpkg-buildpackage -b`)

The wheezy build does not include bladeRF support.

## Building manually

You can probably just run "make" after installing the required dependencies.
Binaries are built in the source directory; you will need to arrange to
install them (and a method for starting them) yourself.

``make BLADERF=no`` will disable bladeRF support and remove the dependency on
libbladeRF.

``make RTLSDR=no`` will disable rtl-sdr support and remove the dependency on 
librtlsdr.
