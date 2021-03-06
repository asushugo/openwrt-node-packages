# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NPM_NAME:=hashmap
PKG_NAME:=node-$(PKG_NPM_NAME)
PKG_VERSION:=2.1.0
PKG_RELEASE:=5

PKG_SOURCE:=$(PKG_NPM_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=http://registry.npmjs.org/$(PKG_NPM_NAME)/-/
PKG_HASH:=600e616ef88d73ad9fb42895c76680d7c5a230e72a51875770f903d6b4a9a936

PKG_BUILD_DEPENDS:=node/host
PKG_USE_MIPS16:=0

PKG_MAINTAINER:=Hirokazu MORIKAWA <morikw2@gmail.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/node-hashmap
  SUBMENU:=Node.js
  SECTION:=lang
  CATEGORY:=Languages
  TITLE:=HashMap Class for JavaScript
  URL:=https://www.npmjs.org/package/hashmap
  DEPENDS:=+node
endef

define Package/node-hashmap/description
 This project provides a HashMap class that works both on Node.js and the browser. HashMap instances store key/value pairs allowing keys of any type
endef

NODEJS_CPU:=$(subst powerpc,ppc,$(subst aarch64,arm64,$(subst x86_64,x64,$(subst i386,ia32,$(ARCH)))))

define Build/Prepare
	$(INSTALL_DIR) $(PKG_BUILD_DIR)
endef

define Build/Compile
	$(MAKE_VARS) \
	$(MAKE_FLAGS) \
	npm_config_arch=$(NODEJS_CPU) \
	npm_config_nodedir=$(STAGING_DIR)/usr/ \
	npm_config_cache=$(TMP_DIR)/npm-cache \
	npm_config_tmp=$(TMP_DIR)/npm-tmp \
	PREFIX="$(PKG_INSTALL_DIR)/usr/" \
	npm install --build-from-source --target_arch=$(NODEJS_CPU) -g $(DL_DIR)/$(PKG_SOURCE)
	rm -rf $(TMP_DIR)/npm-tmp
	rm -rf $(TMP_DIR)/npm-cache
endef

define Package/node-hashmap/install
	$(INSTALL_DIR) $(1)/usr/lib/node
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/node_modules/* $(1)/usr/lib/node/
endef

$(eval $(call BuildPackage,node-hashmap))
