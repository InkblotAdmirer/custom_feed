Custom packages for OpenWRT or LEDE.

Custom feeds are discussed here:  https://wiki.openwrt.org/doc/devel/feeds

PACKAGES

spiped - https://github.com/Tarsnap/spiped
dnscrypt-proxy-v2 - https://github.com/jedisct1/dnscrypt-proxy

spiped notes:

No package for spiped was found, so this was created.  The package is simple and basic but installs and appears to work.

The patches convert makefiles from BSD to POSIX.

The config is loaded in /etc/config/spiped.  Two default configurations are loaded for reference, both disabled.  Multiple instances are allowed.

The init script iterates through the configs and if enabled, starts a daemon.  If the referenced key is not available it is created at this point.

Testing has consisted of tcpdump captures on each of the ports, and information in-the-clear is seen on server target port while it appears encrypted on the source port.

dnscrypt-proxy-v2 notes:

The OpenWRT build system does not currently include the capability to cross-compile Go, so the precompiled ARM binary is downloaded and installed.

The service is started with procd referencing /etc/config/dnscrypt-proxy-v2.toml for configuration.  The included configuration example is installed directly.  The process is run as user nobody in group nogroup, and empty blacklist and cloaking files with these permissions are created in /tmp.  Procd reload triggering is hard coded to "wan" -- this, and other hard-coded configuration settings are planned to be configured via UCI eventually.
