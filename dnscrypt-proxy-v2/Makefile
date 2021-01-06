#
# Copyright (C) 2018-2020 Inkblot Admirer
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=dnscrypt-proxy-v2
PKG_VERSION:=2.0.45
PKG_RELEASE:=1
PKG_MAINTAINER:=Maintainer Name <email@gmail.com>
PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=COPYING

PKG_SOURCE_URL:=https://github.com/DNSCrypt/dnscrypt-proxy/archive/$(PKG_VERSION).tar.gz
PKG_SOURCE:=dnscrypt-proxy-$(PKG_VERSION).tar.gz
PKG_HASH:=f7aac28c6a60404683d436072b89d18ed3bb309f8d8a95c8e87ad250da190821
PKG_BUILD_DIR:=$(BUILD_DIR)/dnscrypt-proxy-$(PKG_VERSION)

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

GO_PKG:=github.com/DNSCrypt/dnscrypt-proxy

include $(INCLUDE_DIR)/package.mk
include ../../packages/lang/golang/golang-package.mk

define Package/dnscrypt-proxy-v2
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=IP Addresses and Names
  TITLE:=A tool for securing communication between a client and a DNS resolver
  URL:=https://github.com/jedisct1/dnscrypt-proxy
  USERID:=nobody=65534:nogroup=65534
  DEPENDS:=$(GO_ARCH_DEPENDS)
  CONFLICTS:=dnscrypt-proxy
endef

define Package/dnscrypt-proxy-v2/description
  A flexible DNS proxy, with support for modern encrypted DNS protocols such as DNSCrypt v2
  and DNS-over-HTTP/2.
endef

define Package/dnscrypt-proxy-v2/conffiles
/etc/dnscrypt-proxy/dnscrypt-proxy.toml
/etc/config/dnscrypt-proxy
endef

define Package/dnscrypt-proxy-v2/install
	$(call GoPackage/Package/Install/Bin,$(PKG_INSTALL_DIR))

	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/sbin/dnscrypt-proxy

	$(INSTALL_DIR) $(1)/etc/dnscrypt-proxy
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/dnscrypt-proxy/example-dnscrypt-proxy.toml \
		$(1)/etc/dnscrypt-proxy/dnscrypt-proxy.toml

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_BIN) ./files/dnscrypt-proxy-v2.conf $(1)/etc/config/dnscrypt-proxy

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/dnscrypt-proxy-v2.init $(1)/etc/init.d/dnscrypt-proxy

endef

$(eval $(call GoBinPackage,dnscrypt-proxy-v2))
$(eval $(call BuildPackage,dnscrypt-proxy-v2))

