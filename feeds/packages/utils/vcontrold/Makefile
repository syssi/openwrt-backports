#
# Copyright (C) 2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=vcontrold
PKG_VERSION:=0.98
PKG_RELEASE=$(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO:=svn
PKG_SOURCE_URL:=https://vcontrold.svn.sourceforge.net/svnroot/vcontrold
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=r33
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

include $(INCLUDE_DIR)/package.mk

MAKE_PATH:=vcontrold
CONFIGURE_PATH:=vcontrold

define Package/vcontrold
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libxml2
  TITLE:=vcontrold is a linux daemon for vito communication
  URL:=http://vcontrold.wikispaces.com/vcontrold
endef

define Package/vcontrold/description
A daemon reading data coming from the control unit of a vito heating
system using an optolink adapter connected to a serial port.
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR)/vcontrold && aclocal && autoconf && touch NEWS README AUTHORS ChangeLog && automake --add-missing)
	$(call Build/Configure/Default, \
		--with-xml2-include-dir=$(STAGING_DIR)/usr/include/libxml2 \
	)
endef

define Package/vcontrold/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/vcontrold/vclient $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/vcontrold/vcontrold $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/vcontrold.init $(1)/etc/init.d/vcontrold

	$(INSTALL_DIR) $(1)/etc/vcontrold
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/vcontrold/vcontrold.xml $(1)/etc/vcontrold/vcontrold_dev-id-2098.xml
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/xml-32/xml/*.{xml,ini} $(1)/etc/vcontrold/
endef

$(eval $(call BuildPackage,vcontrold))
