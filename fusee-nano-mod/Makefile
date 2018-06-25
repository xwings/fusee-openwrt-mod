include $(TOPDIR)/rules.mk

PKG_NAME:=fusee-nano-mod
PKG_VERSION:=0.1
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:= https://github.com/xwings/fusee-nano-mod/archive
PKG_CAT:=zcat

include $(INCLUDE_DIR)/package.mk

define Package/fusee-nano-mod
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=Tiny FG exploit implementation
	URL:=https://github.com/xwings/fusee-nano-mod
endef

define Package/fusee-nano-mod/description
	Tiny FG exploit implementation
endef

define Build/Compile
	$(call Build/Compile/Default,INTERMEZZO=/usr/share/fusee-nano/intermezzo.bin)
endef

define Package/fusee-nano-mod/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/fusee-nano $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/hotplug.d/usb/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/files/20-tegra_rcm $(1)/etc/hotplug.d/usb/
	$(INSTALL_DIR) $(1)/usr/share/fusee-nano/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/files/intermezzo.bin $(1)/usr/share/fusee-nano/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/files/payload.bin $(1)/usr/share/fusee-nano/
endef

$(eval $(call BuildPackage,fusee-nano-mod))
