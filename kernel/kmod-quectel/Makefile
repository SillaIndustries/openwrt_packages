#
# Copyright (C) Silla srl
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=kmod-quectel
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define KernelPackage/kmod-quectel
  SUBMENU:=Other modules
  TITLE:=Quectel driver support
  FILES:=$(PKG_BUILD_DIR)/*.$(LINUX_KMOD_SUFFIX)
  KCONFIG:=
endef

define KernelPackage/kmod-quectel/description
  Kernel module to kmod-quectel
endef

EXTRA_KCONFIG:= \
	CONFIG_EXAMPLE=m

EXTRA_CFLAGS:= \
	$(patsubst CONFIG_%, -DCONFIG_%=1, $(patsubst %=m,%,$(filter %=m,$(EXTRA_KCONFIG)))) \
	$(patsubst CONFIG_%, -DCONFIG_%=1, $(patsubst %=y,%,$(filter %=y,$(EXTRA_KCONFIG)))) \

MAKE_OPTS:= \
	ARCH="$(LINUX_KARCH)" \
	CROSS_COMPILE="$(TARGET_CROSS)" \
	SUBDIRS="$(PKG_BUILD_DIR)" \
	EXTRA_CFLAGS="$(EXTRA_CFLAGS)" \
	$(EXTRA_KCONFIG)

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./src/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		$(MAKE_OPTS) \
		modules
endef

$(eval $(call KernelPackage,kmod-quectel))
