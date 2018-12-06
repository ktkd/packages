#
# Copyright (C) 2007 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# $Id: Makefile 9173 2007-10-07 03:20:26Z blogic $

include $(TOPDIR)/rules.mk

PKG_NAME:=libtorrent-rasterbar
PKG_VERSION:=1.1.9
PKG_RELEASE:=1

PKG_SOURCE:=libtorrent-rasterbar-1.1.9.tar.gz
PKG_SOURCE_URL:=https://github.com/arvidn/libtorrent/releases/download/libtorrent-1_1_9/
PKG_HASH:=d57a0f5b159f58003c3031943463503f0d05ae3e428dd7c2383d1e35fb2c4e8c
PKG_BUILD_DIR:=$(BUILD_DIR)/libtorrent-rasterbar-$(PKG_VERSION)
PKG_BUILD_DEPENDS:=libtool
include $(INCLUDE_DIR)/package.mk

define Package/libtorrent-rasterbar
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Rasterbar BitTorrent library
  URL:=http://www.rasterbar.com/products/libtorrent/
  DEPENDS:=+boost +boost-python3 +boost-filesystem +boost-regex +boost-thread +boost-program_options +boost-system +libopenssl +zlib +boost-random
  MAINTAINER:=Kirill Alexandrovich <ktk@ktkd.ru>
endef

define Package/libtorrent-rasterbar/description
Rasterbar libtorrent is a C++ library that aims to be a good alternative to
all the other bittorrent implementations around. It is a library and not a
full featured client, although it comes with a working example client.
endef

CONFIGURE_ARGS+= \
	--enable-shared \
	--disable-debug \
	--enable-static=no \
	--enable-python-binding \
	--with-sysroot=$(STAGING_DIR)/root-x86 \
	--includedir=$(STAGING_DIR)/usr/include \
	--with-boost \
	--with-boost-libdir=$(STAGING_DIR)/usr/include
#	--enable-tests \
#	--with-boost-libdir=$(STAGING_DIR)/root-x86/usr/lib \
#	--with-zlib=detect \
#	--with-boost-system=boost_system \
#	--with-boost-filesystem=boost_filesystem \
#	--with-boost-thread=boost_thread \
#	--with-boost-regex=boost_regex \
#	--with-boost-python=boost_python \
#	--with-boost-program_options=boost_program_options

CONFIGURE_VARS+=CC="$(TARGET_CXX)"

EXTRA_LDFLAGS+=-lz -lpthread

define Build/Compile
	$(call Build/Compile/Default)
	$(call Build/Install/Default)
endef

define Build/InstallDev
	mkdir -p $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libtorrent $(1)/usr/include/
	mkdir -p $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
	mkdir -p $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libtorrent-rasterbar.pc $(1)/usr/lib/pkgconfig/
endef

define Package/libtorrent-rasterbar/install
	$(INSTALL_DIR) $(1)/usr/lib $(1)/usr/lib/python3.6/site-packages/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/python3.6/site-packages/*.so $(1)/usr/lib/python3.6/site-packages/
endef

$(eval $(call BuildPackage,libtorrent-rasterbar))

