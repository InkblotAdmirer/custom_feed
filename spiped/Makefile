#
# Copyright (C) 2016-2020 Inkblot Admirer
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=spiped
PKG_VERSION:=1.6.1
PKG_RELEASE:=$(PKG_SOURCE_VERSION)
PKG_MAINTAINER:=Maintainer Name <email@gmail.com>
PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=COPYING

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Tarsnap/spiped
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=e56ffd717e9d13c534bbaba3f3515e94e96f4a34
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_HASH:=5b2473ca9826b1801355a1f0a794fd69e8007994407e395a9ea779730b4d3604

PKG_INSTALL:=1
PKG_FIXUP:=autoreconf

# add compiler optimization (last flag on command line is the one used)
TARGET_CFLAGS += -O2

include $(INCLUDE_DIR)/package.mk

define Package/spiped
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libopenssl
  TITLE:=Utility to create encrypted and authenticated pipes
  URL:=http://www.tarsnap.com/spiped.html
  USERID:=spiped=8228:spiped=8228
endef

define Package/spiped/description
  Spiped is a utility for creating symmetrically encrypted and authenticated pipes
  between socket addresses.
endef

define Package/spiped/conffiles
/etc/config/spiped
endef

define Build/Configure
	sed -i 's/@VERSION@/${PKG_VERSION}/g' $(PKG_BUILD_DIR)/spipe/main.c
	sed -i 's/@VERSION@/${PKG_VERSION}/g' $(PKG_BUILD_DIR)/spiped/main.c
	$(call Build/Configure/Default)
endef

define Package/spiped/install
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/spiped.conf $(1)/etc/config/spiped
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/spiped.init $(1)/etc/init.d/spiped
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/spipe $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/spiped $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,spiped))
