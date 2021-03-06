include $(TOPDIR)/rules.mk

PKG_NAME:=letmecreate
PKG_VERSION:=1.2.1

PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/francois-berder/LetMeCreate.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

PKG_LICENSE_FILE:=LICENSE
PKG_LICENSE:=BSD-3-Clause
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/letmecreate
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=LetMeCreate
  DEPENDS:=@TARGET_pistachio
endef

define Package/letmecreate/description
 This library is a collection of wrappers for interfaces of the Ci40. It also
 contains drivers for some Click boards. Examples are installed in
 /usr/bin/letmecreate_examples.
endef

define Package/letmecreate/config
	source "$(SOURCE)/Config.in"
endef

CMAKE_OPTIONS += $(if $(CONFIG_LETMECREATE_BUILD_EXAMPLES),-DBUILD_EXAMPLES=ON)

define Build/InstallDev
	$(INSTALL_DIR) $(STAGING_DIR)/usr/include/letmecreate
	$(CP) $(PKG_INSTALL_DIR)/usr/include/letmecreate $(STAGING_DIR)/usr/include/

	$(INSTALL_DIR) $(STAGING_DIR)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so $(STAGING_DIR)/usr/lib/

	$(INSTALL_DIR) $(STAGING_DIR)/usr/lib/cmake/LetMeCreate
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/LetMeCreate/*.cmake $(STAGING_DIR)/usr/lib/cmake/LetMeCreate
endef

define Package/letmecreate/install
	if [ -d "$(PKG_BUILD_DIR)/examples/bin/" ]; then \
		mkdir -p $(1)/usr/bin/letmecreate_examples; \
		$(INSTALL_BIN) $(PKG_BUILD_DIR)/examples/bin/* $(1)/usr/bin/letmecreate_examples; \
		mkdir -p $(1)/usr/bin/letmecreate_examples/data; \
		$(INSTALL_DATA) $(PKG_BUILD_DIR)/examples/data/* $(1)/usr/bin/letmecreate_examples/data; \
	fi

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/include/letmecreate
	$(CP) $(PKG_INSTALL_DIR)/usr/include/* $(1)/usr/include/

	$(INSTALL_DIR) $(1)/usr/lib/cmake/LetMeCreate
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/LetMeCreate/*.cmake $(1)/usr/lib/cmake/LetMeCreate
endef

$(eval $(call BuildPackage,letmecreate))
