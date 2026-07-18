include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-openclash
PKG_VERSION:=0.47.116
PKG_RELEASE:=1
PKG_SOURCE:=OpenClash-v$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/vernesong/OpenClash/archive/refs/tags/v$(PKG_VERSION).tar.gz?
PKG_HASH:=3253dd3d1f12a197936098c2c5f162ab813a27bf03938a991a323b24fdeb9520
PKG_BUILD_DIR:=$(BUILD_DIR)/OpenClash-$(PKG_VERSION)/luci-app-openclash

PKG_MAINTAINER:=vernesong <https://github.com/vernesong/OpenClash>
PKG_LICENSE:=MIT

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)/config
	config PACKAGE_kmod-inet-diag
	default y if PACKAGE_$(PKG_NAME)

	config PACKAGE_luci-compat
	default y if PACKAGE_$(PKG_NAME)

	config PACKAGE_kmod-nft-tproxy
	default y if PACKAGE_firewall4

	config PACKAGE_kmod-ipt-nat
	default y if !PACKAGE_firewall4

	config PACKAGE_iptables-mod-tproxy
	default y if !PACKAGE_firewall4

	config PACKAGE_iptables-mod-extra
	default y if !PACKAGE_firewall4

	config PACKAGE_dnsmasq_full_ipset
	default y if !PACKAGE_firewall4

	config PACKAGE_dnsmasq_full_nftset
	default y if PACKAGE_firewall4

	config PACKAGE_ipset
	default y if !PACKAGE_firewall4
endef

define Package/$(PKG_NAME)
	CATEGORY:=LuCI
	SUBMENU:=3. Applications
	TITLE:=LuCI support for Mihomo
	PKGARCH:=all
	DEPENDS:=+dnsmasq-full +bash +curl +ca-bundle +ip-full \
		+ruby +ruby-yaml +kmod-tun +unzip +openclash-core
endef

define Package/$(PKG_NAME)/description
	OpenClash LuCI application, pinned to a verified upstream release.
endef

define Build/Configure
endef

define Build/Compile
	$(foreach po,$(wildcard $(PKG_BUILD_DIR)/po/zh-cn/*.po), \
		po2lmo $(po) $(PKG_BUILD_DIR)/$(patsubst %.po,%.lmo,$(notdir $(po)));)
	chmod 0755 $(PKG_BUILD_DIR)/root/etc/init.d/openclash
	chmod -R 0755 $(PKG_BUILD_DIR)/root/usr/share/openclash/
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/i18n
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/*.*.lmo $(1)/usr/lib/lua/luci/i18n/
	$(CP) $(PKG_BUILD_DIR)/root/* $(1)/
	$(CP) $(PKG_BUILD_DIR)/luasrc/* $(1)/usr/lib/lua/luci/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
