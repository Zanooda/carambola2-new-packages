#
# Copyright (C) 2006-2009 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=haserl
PKG_VERSION:=0.9.32
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/haserl
PKG_MD5SUM:=18e2208aea6d772d1670c1a648bb6b77
PKG_MAINTAINER:=Maxim Storchak <m.storchak@gmail.com>
PKG_LICENSE:=GPL-2.0

include $(INCLUDE_DIR)/package.mk

define Package/haserl
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=A CGI wrapper to embed shell scripts in HTML documents
  URL:=http://haserl.sourceforge.net/
  MENU:=1
  DEPENDS:= +HASERL_with_lua:liblua
endef

define Package/haserl/config
	source "$(SOURCE)/Config.in"
endef

ifeq ($(CONFIG_HASERL_with_lua),y)
	CONFIGURE_ARGS+=--with-lua
	TARGET_LDFLAGS += -ldl
endif
ifneq ($(CONFIG_HASERL_shell_lua),y)
	CONFIGURE_ARGS+=--disable-luashell
endif
ifneq ($(CONFIG_HASERL_shell_luac),y)
	CONFIGURE_ARGS+=--disable-luacshell
endif

define Package/haserl/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/haserl $(1)/usr/bin/
endef

$(eval $(call BuildPackage,haserl))
