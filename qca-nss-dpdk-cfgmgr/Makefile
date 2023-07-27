include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=qca-nss-dpdk-cfgmgr
PKG_VERSION:=1.0
PKG_RELEASE:=$(AUTORELEASE)

PKG_SRC_DIR=$(TOPDIR)/qca/src/qca-nss-dpdk-cfgmgr

include $(INCLUDE_DIR)/local-development.mk
include $(INCLUDE_DIR)/package.mk

define KernelPackage/$(PKG_NAME)
  SECTION:=kernel
  CATEGORY:=Kernel modules
  SUBMENU:=Network Devices
  TITLE:=Kernel Module for DPDK Router Configuration Manager
  FILES:=$(PKG_BUILD_DIR)/qca-nss-dpdk-cfgmgr.ko
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) $(PKG_SRC_DIR)/Makefile $(PKG_BUILD_DIR)
	$(CP) $(PKG_SRC_DIR)/src/* $(PKG_BUILD_DIR)
endef

define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" $(strip $(MAKE_OPTS)) \
		CROSS_COMPILE="$(TARGET_CROSS)" \
		ARCH="$(LINUX_KARCH)" \
		M="$(PKG_BUILD_DIR)" \
		EXTRA_CFLAGS="$(EXTRA_CFLAGS)" \
		SoC="$(subtarget)" \
		modules
endef

define KernelPackage/$(PKG_NAME)/install
	$(CP) $(PKG_BUILD_DIR)/qca-nss-dpdk-cfgmgr.ko $(TARGET_DIR)/$(MODULES_SUBDIR)
endef

define KernelPackage/$(PKG_NAME)/Description
	Config Manager kernel netlink module (qca-nss-dpdk-cfgmgr.ko) if for processing
	user requests and send post routing infomration to PP client application in user space
	to add/delete a routing entry.
endef

$(eval $(call KernelPackage,$(PKG_NAME)))
