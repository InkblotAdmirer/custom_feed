#
# Copyright (C) 2020 Inkblot Admirer
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=nethogs
PKG_VERSION:=0.8.6
PKG_RELEASE:=$(PKG_SOURCE_VERSION)
PKG_MAINTAINER:=Maintainer Name <email@gmail.com>
PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=COPYING

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/raboof/nethogs
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=3889d20018b9d9a27c86efb4c8a06c2106aaf2c2
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_HASH:=9e472a5b612f6b398342b72d692326cdb275825359424195d041d87abc33087c

PKG_INSTALL:=1
PKG_FIXUP:=autoreconf

# add compiler optimization (last flag on command line is the one used)
TARGET_CFLAGS += -O2

include $(INCLUDE_DIR)/package.mk

define Package/nethogs
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libpcap +libncurses +libstdcpp
  TITLE:=Nethogs is a small net top tool.
  URL:=https://github.com/raboof/nethogs
endef

define Package/nethogs/description
  NetHogs is a small 'net top' tool. Instead of breaking the traffic down per protocol
  or per subnet, like most tools do, it groups bandwidth by process.
endef

define Build/Configure
	sed -i 's/VERSION := .*/VERSION := ${PKG_VERSION}/' ${PKG_BUILD_DIR}/Makefile
	$(call Build/Configure/Default)
endef

define Package/nethogs/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/local/sbin/nethogs $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,nethogs))
