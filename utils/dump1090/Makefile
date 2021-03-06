#
# Copyright (C) 2013-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=dump1090
PKG_VERSION:=2014-07-25
PKG_RELEASE:=$(PKG_SOURCE_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://github.com/MalcolmRobb/dump1090.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=a17e5b0f980f726d246ee5c8fe1661c99a11e90f
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_MAINTAINER:=Álvaro Fernández Rojas <noltari@gmail.com>

PKG_LICENSE:=BSD-3c

include $(INCLUDE_DIR)/package.mk

define Package/dump1090
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Mode S decoder for the Realtek RTL2832U
  URL:=https://github.com/antirez/dump1090
  DEPENDS:=+libpthread +librtlsdr
endef

define Package/dump1090/config
	source "$(SOURCE)/Config.in"
endef

define Package/dump1090/description
 Dump1090 is a Mode S decoder specifically designed for RTLSDR devices.
 Embedded HTTP server that displays the currently detected aircrafts on
 Google Maps. Network output in Basestation and AVR formats.
endef

MAKE_FLAGS += \
	CFLAGS="$(TARGET_CFLAGS)"

define Package/dump1090/install
	$(INSTALL_DIR) $(1)/usr/bin

ifneq ($(CONFIG_DUMP1090_DUMP),)
	$(CP) $(PKG_BUILD_DIR)/dump1090 $(1)/usr/bin
ifneq ($(CONFIG_DUMP1090_WWW),)
	$(INSTALL_DIR) $(1)/usr/share/dump1090
	$(CP) $(PKG_BUILD_DIR)/public_html/* $(1)/usr/share/dump1090
endif
endif
ifneq ($(CONFIG_DUMP1090_VIEW),)
	$(CP) $(PKG_BUILD_DIR)/view1090 $(1)/usr/bin
endif
endef

$(eval $(call BuildPackage,dump1090))
