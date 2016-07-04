# Cups image

## Overview

Docker image including Cups 1.5.3 and Printing drivers (installed from the
Debian oldstable packages).
This image is designed to run an old cups in parallel with a recent version on
a server to support users with old version of cups.

## Run the Cups server
```bash
docker run -d --privileged -v /dev/bus/usb/:/dev/bus/usb/ -v /var/run/dbus/:/var/run/dbus/ --net=host --name dbeniamine/docker-debian-cups
```
__Note__:

* The admin user/password for the Cups server is `print`/`print`
* The  `--privileged -v /dev/bus/usb/:/dev/bus/usb/` is only required for usb
  printers

## Add printers to the Cups server
1. Connect to the Cups server at [http://127.0.0.1:6631](http://127.0.0.1:6631)
2. Add printers: Administration > Printers > Add Printer
3. (The user/password is `print`/`print`)

## Configure Cups (<1.6) client

1.  Install the `cups-client` package
2.  Add the following lines to `/etc/cups/cups.d.conf`:

        BrowseAllow <Hostname>:6631
        BrowsePoll <Hostname>:6631

    Where `<Hostname>` is the name of the server that runs the docker
    container.
3. Restart cups `sudo service cups restart`
4. The printers from cups 1.5.3 should appears

### Included package
* cups, cups-client
* printer-driver-all
* hpijs-ppds, hp-ppd
* sudo, locales, whois, vim
