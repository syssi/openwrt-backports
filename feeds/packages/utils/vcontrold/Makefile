#
# Copyright (C) 2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=vcontrold
PKG_VERSION:=0.98.11

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL=https://github.com/openv/vcontrold.git
PKG_SOURCE_DATE:=2021-04-18
PKG_SOURCE_VERSION:=977e6f5da497be8334cb75a99b311d11dea972b3
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_MIRROR_HASH=02689236ad9a97440d8edf9dcc4ac45a02c5135757e52292036fd749f660aff6
CMAKE_INSTALL:=1
CMAKE_OPTIONS += -DMANPAGES=OFF

PKG_LICENSE:=GPL-3.0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/vcontrold
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libxml2
  TITLE:=vcontrold is a linux daemon for vito communication
  URL:=https://github.com/openv/vcontrold
endef

define Package/vcontrold/description
A daemon reading data coming from the control unit of a vito heating
system using an optolink adapter connected to a serial port.
endef

define Package/vcontrold/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/vclient $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/vcontrold $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/vcontrold.init $(1)/etc/init.d/vcontrold

	$(INSTALL_DIR) $(1)/etc/vcontrold
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/xml/300/* $(1)/etc/vcontrold/
	$(INSTALL_DIR) $(1)/etc/vcontrold/kw
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/xml/kw/* $(1)/etc/vcontrold/kw/
endef

$(eval $(call BuildPackage,vcontrold))
