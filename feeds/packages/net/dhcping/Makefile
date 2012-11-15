include $(TOPDIR)/rules.mk

PKG_NAME:=dhcping
PKG_VERSION:=1.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.mavetju.org/download/
PKG_MD5SUM:=c4b22bbf3446c8567e371c40aa552d5d

include $(INCLUDE_DIR)/package.mk

define Package/dhcping
       SECTION:=net
       CATEGORY:=Network
       TITLE:=DHCP Daemon Ping Program
endef

define Package/dhcping/description
This small tool provides an opportunity for a system administrator to
perform a DHCP request to find out if a DHCP server is still running.
endef

#TARGET_CFLAGS += -I$(STAGING_DIR)/usr/include
#TARGET_CFLAGS += -ggdb3
#CMAKE_OPTIONS += -DDEBUG=1

define Package/dhcping/install
       $(INSTALL_DIR) $(1)/usr/sbin
       $(INSTALL_BIN) $(PKG_BUILD_DIR)/dhcping $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,dhcping))

