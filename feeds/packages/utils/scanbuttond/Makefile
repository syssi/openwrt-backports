include $(TOPDIR)/rules.mk

PKG_NAME:=scanbuttond
PKG_VERSION:=0.2.3
PKG_RELEASE:=cvs20090713-9-debian

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/scanbuttond
PKG_MD5SUM:=548e6451b398bd95d14f008b4d39ca79

PKG_FIXUP:=autoreconf

TARGET_CFLAGS += -D_GNU_SOURCE

include $(INCLUDE_DIR)/package.mk

define Package/scanbuttond
	SECTION:=utils
	CATEGORY:=Utilities
	DEPENDS:=+libusb
	TITLE:=Scanner button daemon
endef

define Package/scanbuttond/description
It allows you to invoke actions such as shell scripts whenever one of
the scanner front panel buttons is pressed.
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

