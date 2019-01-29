#
# Copyright (C) 2010-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=imagemagick
PKG_VERSION:=7.0.8
PKG_REVISION:=23
PKG_RELEASE:=2

PKG_BUILD_DIR:=$(BUILD_DIR)/ImageMagick-$(PKG_VERSION)-$(PKG_REVISION)
PKG_SOURCE:=ImageMagick-$(PKG_VERSION)-$(PKG_REVISION).tar.xz
PKG_SOURCE_URL:=ftp://ftp.fifi.org/pub/ImageMagick/
#PKG_MD5SUM:=c66bea4710370b2e115aed512fbe4601

PKG_FIXUP:=autoreconf
PKG_REMOVE_FILES:=aclocal.m4 m4/libtool.m4
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

PKG_INSTALL=1

define Package/imagemagick/Default
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=imagemagick
  URL:=http://image_magick.veidrodis.com/
endef

define Package/imagemagick
  $(call Package/imagemagick/Default)
  DEPENDS:=+libpthread +libltdl +libjpeg +libtiff +zlib +liblzma +libfreetype +libpng

endef

define Package/imagemagick/description
  An image manipulation library.
endef


define Package/imagemagick-tools
  $(call Package/imagemagick/Default)
  TITLE+= (tools)
  DEPENDS:=+imagemagick
endef


CONFIGURE_ARGS += \
	--with-modules \
	--with-quantum-depth=8 \
	--enable-shared \
	--enable-static \
	--disable-hdri \
	--without-bzlib \
	--without-rsvg \
	--without-x\
	--without-magick-plus-plus\
	--with-xml=no \
	--with-fftw=yes \
	--with-fontconfig=yes \
	--with-pango=yes \
	--with-djvu=yes \
	--with-wmf=yes
#	--without-freetype \

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		CFLAGS="$(TARGET_CFLAGS) -Wall -I$(PKG_BUILD_DIR)/include/linux -I$(PKG_BUILD_DIR)/include -I$(STAGING_DIR)/usr/include\
		 -I$(STAGING_DIR)/usr/include/freetype2"
endef


define Package/imagemagick/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/*.so* \
		$(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/ImageMagick-$(PKG_VERSION)/config-Q8/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/ImageMagick-$(PKG_VERSION)/config-Q8/*.xml \
		$(1)/usr/lib/ImageMagick-$(PKG_VERSION)/config-Q8/

	$(INSTALL_DIR) $(1)/usr/lib/ImageMagick-$(PKG_VERSION)/modules-Q8/coders
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/ImageMagick-$(PKG_VERSION)/modules-Q8/coders/*.so \
		$(1)/usr/lib/ImageMagick-$(PKG_VERSION)/modules-Q8/coders/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/ImageMagick-$(PKG_VERSION)/modules-Q8/coders/*.la \
		$(1)/usr/lib/ImageMagick-$(PKG_VERSION)/modules-Q8/coders/

	$(INSTALL_DIR) $(1)/usr/lib/ImageMagick-$(PKG_VERSION)/modules-Q8/filters
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/ImageMagick-$(PKG_VERSION)/modules-Q8/filters/*.so \
		$(1)/usr/lib/ImageMagick-$(PKG_VERSION)/modules-Q8/filters/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/ImageMagick-$(PKG_VERSION)/modules-Q8/filters/*.la \
		$(1)/usr/lib/ImageMagick-$(PKG_VERSION)/modules-Q8/filters/


	$(INSTALL_DIR) $(1)/usr/share/ImageMagick-7/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/share/ImageMagick-7/*.xml \
		$(1)/usr/share/ImageMagick-7/

	$(INSTALL_DIR) $(1)/etc/ImageMagick-7/
	$(CP) \
		$(PKG_INSTALL_DIR)/etc/ImageMagick-7/*.xml \
		$(1)/etc/ImageMagick-7/
endef

define Package/imagemagick-tools/install
	$(INSTALL_DIR) $(1)/usr/bin/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/bin/magick \
		$(1)/usr/bin/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/bin/animate \
		$(1)/usr/bin/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/bin/compare \
		$(1)/usr/bin/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/bin/composite \
		$(1)/usr/bin/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/bin/conjure \
		$(1)/usr/bin/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/bin/convert \
		$(1)/usr/bin/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/bin/display \
		$(1)/usr/bin/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/bin/identify \
		$(1)/usr/bin/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/bin/import \
		$(1)/usr/bin/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/bin/mogrify \
		$(1)/usr/bin/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/bin/montage \
		$(1)/usr/bin/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/bin/stream \
		$(1)/usr/bin/
endef



$(eval $(call BuildPackage,imagemagick))
$(eval $(call BuildPackage,imagemagick-tools))

