include $(TOPDIR)/rules.mk

PKG_NAME:=scanbuttond
PKG_UPSTREAM_VERSION:=0.2.3
# Debian patch level: 0.2.3.cvs20090713-9
PKG_VERSION:=$(PKG_UPSTREAM_VERSION)_cvs20090713
# r10: + patch 020 (rename internal libusb_* → libusbi_, symbol clash with libusb-1.0)
PKG_RELEASE:=10

PKG_SOURCE:=$(PKG_NAME)-$(PKG_UPSTREAM_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/scanbuttond
PKG_HASH:=93b060a363fef069548a49cb151da53ac6071dc0569f9a07d68751a28dffebee
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_UPSTREAM_VERSION)

PKG_LICENSE:=GPL-2.0-or-later
PKG_FIXUP:=autoreconf

TARGET_CFLAGS += -D_GNU_SOURCE

include $(INCLUDE_DIR)/package.mk

define Package/scanbuttond
	SECTION:=utils
	CATEGORY:=Utilities
	DEPENDS:=+libusb-compat
	TITLE:=Scanner button daemon
	URL:=https://scanbuttond.sourceforge.net/
endef

define Package/scanbuttond/description
It allows you to invoke actions such as shell scripts whenever one of
the scanner front panel buttons is pressed.
endef

define Package/scanbuttond/conffiles
/etc/scanbuttond/meta.conf
endef

define Package/scanbuttond/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/scanbuttond $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/backends/.libs/libscanbtnd-backend*.so* $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/interface/.libs/libscanbtnd-interface*.so* $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/etc/scanbuttond
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/scripts/*.example $(1)/etc/scanbuttond/
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/backends/*.conf $(1)/etc/scanbuttond/

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/scanbuttond.init $(1)/etc/init.d/scanbuttond
endef

$(eval $(call BuildPackage,scanbuttond))
