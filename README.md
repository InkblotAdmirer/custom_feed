Custom packages for OpenWRT or LEDE.

Custom feeds are discussed here:  https://wiki.openwrt.org/doc/devel/feeds

PACKAGES

spiped - https://github.com/Tarsnap/spiped

No package for spiped was found, so this was created.  The package is simple and basic but installs and appears to work.

The patches convert makefiles from BSD to POSIX.

The config is loaded in /etc/config/spiped.  Two default configurations are loaded for reference, both disabled.  Multiple instances are allowed.

The init script iterates through the configs and if enabled, starts a daemon.  If the referenced key is not available it is created at this point.

Testing has consisted of tcpdump captures on each of the ports, and information in-the-clear is seen on server target port while it appears encrypted on the source port.

