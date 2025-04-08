#
# Copyright (C) 2020 Inkblot Admirer
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=nethogs
PKG_VERSION:=0.8.8
PKG_RELEASE:=$(PKG_SOURCE_VERSION)
PKG_MAINTAINER:=Maintainer Name <email@gmail.com>
PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=COPYING

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/raboof/nethogs
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=ea161b050991b92f8d17e6fb6fb4cfae8cf1915d
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_HASH:=111ade20cc545e8dfd7ce4e293bd6b31cd1678a989b6a730bd2fa2acc6254818

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
