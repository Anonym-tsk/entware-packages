#
# Copyright (C) 2015, 2016 gxcreator
# Copyright (C) 2017 OpenWrt.org
# Copyright (C) 2021-2023 PurpleI2P team
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# boost bumped

include $(TOPDIR)/rules.mk

PKG_NAME:=i2pd
PKG_VERSION:=2.50.2
PKG_RELEASE:=2
PKG_BUILD_PARALLEL:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/PurpleI2P/i2pd/tar.gz/$(PKG_VERSION)?
PKG_HASH:=ae2ec4732c38fda71b4b48ce83624dd8b2e05083f2c94a03d20cafb616f63ca5

PKG_MAINTAINER:=David Yang <mmyangfl@gmail.com>
PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE
PKG_CPE_ID:=cpe:/a:i2pd:i2pd

include $(INCLUDE_DIR)/package.mk

define Package/i2pd
	SECTION:=net
	CATEGORY:=Network
	DEPENDS:=+libopenssl +boost +boost-system +boost-filesystem \
	         +boost-program_options +boost-date_time +libatomic +zlib
	TITLE:=full-featured C++ implementation of I2P client
	URL:=https://github.com/PurpleI2P/i2pd
	USERID:=i2pd:i2pd
endef

define Package/i2pd/description
  I2P (Invisible Internet Protocol) is a universal anonymous network layer. All
  communications over I2P are anonymous and end-to-end encrypted, participants
  don't reveal their real IP addresses.
endef

TARGET_LDFLAGS+=-latomic

define Package/i2pd/conffiles
/opt/etc/config/i2pd
/opt/etc/i2pd/i2pd.conf
/opt/etc/i2pd/tunnels.conf
/opt/etc/i2pd/tunnels.d/*
endef

define Package/i2pd/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/i2pd $(1)/opt/sbin
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/i2pd.init-entware $(1)/opt/etc/init.d/S30i2pd
	$(INSTALL_DIR) $(1)/opt/share/i2pd
	$(CP) $(PKG_BUILD_DIR)/contrib/certificates $(1)/opt/share/i2pd
	$(INSTALL_DIR) $(1)/opt/etc/config
	$(INSTALL_CONF) ./files/i2pd.config-entware $(1)/opt/etc/config/i2pd
	$(INSTALL_DIR) $(1)/opt/etc/i2pd
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/contrib/i2pd.conf $(1)/opt/etc/i2pd
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/contrib/tunnels.conf $(1)/opt/etc/i2pd
	# subscriptions.txt deprecated, see #8088
	$(INSTALL_DIR) $(1)/opt/etc/i2pd/tunnels.d
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/contrib/tunnels.d/README $(1)/opt/etc/i2pd/tunnels.d
endef

$(eval $(call BuildPackage,i2pd))
