#
# Copyright 2023 Westermo AG
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cst
PKG_VERSION:=LSDK-21.08
PKG_RELEASE:=$(AUTORELEASE)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/nxp-qoriq/cst
PKG_SOURCE_VERSION:=LSDK-21.08
PKG_MIRROR_HASH:=6ae8a61e659c83b31e05891f33706cc51be6e9b211b7b6e574052aa22a8b095f

include $(INCLUDE_DIR)/host-build.mk

HOST_CFLAGS += -Wall -pedantic -std=c99
define Host/Compile
	#cd $(HOST_BUILD_DIR)/code/cst && $(MAKE) OSTYPE=linux64 ENCRYPTION=yes COPTIONS="${HOST_CFLAGS}" LDOPTIONS="${HOST_LDFLAGS}"
	$(MAKE) -C $(HOST_BUILD_DIR) \
		OPENSSL_INC_PATH="$(STAGING_DIR_HOST)/include/openssl" \
		LDFLAGS="$(HOST_LDFLAGS)"

endef

define Host/Install
	$(CP) \
		$(HOST_BUILD_DIR)/create_hdr_isbc $(HOST_BUILD_DIR)/create_hdr_esbc $(HOST_BUILD_DIR)/create_hdr_pbi $(HOST_BUILD_DIR)/create_hdr_cf \
		$(HOST_BUILD_DIR)/gen_keys $(HOST_BUILD_DIR)/gen_otpmk_drbg $(HOST_BUILD_DIR)/gen_drv_drbg $(HOST_BUILD_DIR)/gen_sign \
		$(HOST_BUILD_DIR)/sign_embed $(HOST_BUILD_DIR)/gen_fusescr \
		$(STAGING_DIR_HOST)/bin/

endef

$(eval $(call HostBuild))
