include $(TOPDIR)/rules.mk

PKG_NAME:=cpufrequtils
PKG_VERSION:=008
PKG_RELEASE:=1
PKG_BUILD_PARALLEL:=1

PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=COPYING
PKG_MAINTAINER:=OpenWrt Contributor

include $(INCLUDE_DIR)/package.mk

PKG_SOURCE_DIR:=$(CURDIR)/../../..

define Package/libcpufreq
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=CPU frequency transition library
endef

define Package/libcpufreq/description
  Shared library used by cpufreq utilities to query and set CPU frequency.
endef

define Package/cpufrequtils
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=CPU frequency setting tools
  DEPENDS:=+libcpufreq
endef

define Package/cpufrequtils/description
  Command line tools for querying and changing CPU frequency scaling settings.
endef

MAKE_FLAGS += \
	CC="$(TARGET_CC)" \
	AR="$(TARGET_AR)" \
	RANLIB="$(TARGET_RANLIB)" \
	STRIP="$(TARGET_CROSS)strip" \
	CFLAGS="$(TARGET_CFLAGS) $(TARGET_CPPFLAGS)" \
	LDFLAGS="$(TARGET_LDFLAGS)" \
	NLS=false \
	CPUFRQ_BENCH=false \
	PROC=false \
	SYSFS=true \
	DEBUG=false

define Build/Prepare
	$(RM) -r $(PKG_BUILD_DIR)
	$(INSTALL_DIR) $(PKG_BUILD_DIR)
	$(CP) $(PKG_SOURCE_DIR)/AUTHORS $(PKG_BUILD_DIR)/
	$(CP) $(PKG_SOURCE_DIR)/COPYING $(PKG_BUILD_DIR)/
	$(CP) $(PKG_SOURCE_DIR)/Makefile $(PKG_BUILD_DIR)/
	$(CP) $(PKG_SOURCE_DIR)/README $(PKG_BUILD_DIR)/
	$(CP) $(PKG_SOURCE_DIR)/build $(PKG_BUILD_DIR)/
	$(CP) $(PKG_SOURCE_DIR)/lib $(PKG_BUILD_DIR)/
	$(CP) $(PKG_SOURCE_DIR)/man $(PKG_BUILD_DIR)/
	$(CP) $(PKG_SOURCE_DIR)/po $(PKG_BUILD_DIR)/
	$(CP) $(PKG_SOURCE_DIR)/utils $(PKG_BUILD_DIR)/
endef

define Build/Compile
	$(call Build/Compile/Default)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include $(1)/usr/lib
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/lib/cpufreq.h $(1)/usr/include/
	$(CP) $(PKG_BUILD_DIR)/libcpufreq.so* $(1)/usr/lib/
endef

define Package/libcpufreq/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/libcpufreq.so.* $(1)/usr/lib/
endef

define Package/cpufrequtils/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/cpufreq-info $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/cpufreq-set $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/cpufreq-aperf $(1)/usr/bin/
endef

$(eval $(call BuildPackage,libcpufreq))
$(eval $(call BuildPackage,cpufrequtils))
