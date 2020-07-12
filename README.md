Custom packages for OpenWRT or LEDE.

Custom feeds are discussed here:  https://wiki.openwrt.org/doc/devel/feeds

PACKAGES

spiped - https://github.com/Tarsnap/spiped
dnscrypt-proxy-v2 - https://github.com/jedisct1/dnscrypt-proxy
nethogs - https://github.com/raboof/nethogs

spiped notes:

No package for spiped was found, so this was created.  The package is simple and basic but installs and appears to work.

The patches convert makefiles from BSD to POSIX.

The config is loaded in /etc/config/spiped.  Two default configurations are loaded for reference, both disabled.  Multiple instances are allowed.

The init script iterates through the configs and if enabled, starts a daemon.  If the referenced key is not available it is created at this point.

Testing has consisted of tcpdump captures on each of the ports, and information in-the-clear is seen on server target port while it appears encrypted on the source port.

dnscrypt-proxy-v2 notes:

As of 2.0.39 Go is used to compile from source.  If not already installed, execute "./scripts/feeds install golang" from the OpenWRT source directory.

Prior to version 2.0.39: The OpenWRT build system does not currently include the capability to cross-compile Go, so the precompiled ARM binary is downloaded and installed.

NOTE: the latest commit is now backward feature-compatible with the original dnscrypt-proxy package, so it is converted to run as dnscrypt-proxy instead of dnscrypt-proxy-v2.  Installs from previous versions will likely require manual intervention after install (i.e. removal of extra files, update of configuration files).  Note that the non-UCI configuration files are to be located in /etc/dnscrypt-proxy.

Source configuration files are copied from /etc/dnscrypt-proxy into /var/etc/dnscrypt, and modified there (UCI-configurable parameters) as necessary.  The service is started with procd referencing the copies in /var/etc/dnscrypt/dnscrypt-proxy.  Configuration options not available in /etc/config/dnscrypt-proxy may be modified in /etc/dnscrypt-proxy/dnscrypt-proxy.toml.

The process is run as user nobody in group nogroup and will listen on 127.0.0.1:5353 by default (no IPv6, to be compatible with baseline v1 installs).

Blacklist and cloaking configuration files should be placed in /etc/dnscrypt-proxy.  These should contain *blacklist* and *cloaking* in the names, as changes to these files are copied back to the configuration folder on stop or shutdown, to preserve across runs.  Note that the blacklist file will be copied into /var/etc/dnscrypt and sourced from there and the log file will be located at the patch specified in the UCI config blacklist list.  The syntax is kept common with the original dnscrypt-proxy which presents a challenge as the parsing must now be in the init script rather than in the dnscrypt-proxy program itself.  As such, there are the currently supported blacklist configurations:
	1) a single blacklist file, either domain or IP
	2) a single blacklist file, either domain or IP with a corresponding log file
	3) two blacklist files, one domain and one IP
	4) two blacklist files, both with a corresponding log file
Any combination other than this will result in undefined behavior.

Downloaded resolver lists and signature files are also copied to the /etc/dnscrypt-proxy configuration folder to preserve across restarts/reloads.

Procd reload triggering is configured in /etc/config as a list with a default of "wan".

nethogs notes:

No package for nethogs was found, so this was created.  The package is simple and basic but installs and appears to work.

The initial version committed is 0.8.6.  Caution may be warranted as this package installs an executable that will run as the user calling it -- if logged in as root, it will run as root.
