#
# Copyright (C) 2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=poppler
PKG_VERSION:=22.12.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://poppler.freedesktop.org/
PKG_MD5SUM:=39b6a69eceba6adb8afbcee8d47385fd

PKG_INSTALL:=1

#CMAKE_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/poppler
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Poppler PDF rendering library
  DEPENDS:=+libpng +libtiff +libjpeg +zlib +lcms2 +fontconfig +libpthread +libfreetype +libstdcpp
  URL:=http://poppler.freedesktop.org/
  SUBMENU:=Printing
endef

define Package/poppler/description
	Poppler is a PDF rendering library based on the xpdf-3.0 code base.
endef

CMAKE_OPTIONS += \
	-DENABLE_X11=OFF \
	-DENABLE_GTK_DOC=OFF \
	-DENABLE_QT5=OFF \
	-DENABLE_QT6=OFF \
	-DENABLE_CPP=ON \
	-DENABLE_ZLIB=ON \
	-DENABLE_LIBJPEG=ON \
	-DENABLE_CMS=lcms2 \
	-DWITH_FONT_CONFIGURATION=fontconfig \
	-DENABLE_UNSTABLE_API_ABI_HEADERS=ON \
	-DENABLE_BOOST=OFF \
  -DENABLE_LIBOPENJPEG=none
 

define Package/poppler/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/cpp $(1)/usr/lib
	$(CP) -r $(PKG_INSTALL_DIR)/usr/include/poppler $(1)/usr/include/
	$(CP) -r $(PKG_BUILD_DIR)/cpp/poppler-version.h $(1)/usr/include/cpp
	$(CP) -r $(PKG_BUILD_DIR)/cpp/poppler-global.h $(1)/usr/include/cpp
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib
endef

$(eval $(call BuildPackage,poppler))
